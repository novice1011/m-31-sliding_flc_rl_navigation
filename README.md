# Sliding Fuzzy Reinforcement learning for navigation README  

"Differential drive mobile robot to approach point using reinforcement learning"  

For better look check this note, please visit [HackMD.io](https://hackmd.io/@libernormous/sliding_flc_rl_nav)  

by:  
[Liber Normous](https://hackmd.io/@libernormous)   

---

# Tutorial  
1. For testing, open `testing.m` and run.  
2. For training, open `training.m`.
    1. change `mode=1` to approach point.  
    2. change `mode=2` to follow point array.  
4. To follow path, use `path_generator.m` to generate point array.  
5. [The latest weight is needed for testing](https://drive.google.com/drive/folders/1GakMGuAzcj2JQt4Hj8VKD2O0YaDnvsfv?usp=sharing)

---

# System description  

This project is developed from our previous project. [It can be seen here.](https://hackmd.io/@libernormous/fuzzy_rl_nav)   

## Robot dynamic    
The robot dynamic can be seen [here ![](https://i.imgur.com/RmvkGxz.png)
](https://hackmd.io/@libernormous/dynamic_ddmr).  

## Reinforcement agent  
![](https://i.imgur.com/Po7hOB6.png)  

### State  
1. 11 sliding position error fuzzy membership fuction  
2. 11 sliding position heading fuzzy membership fuction  

The inputs are fuzzified version of $S_{e_h}, \dot{S}_{e_h}, S_{e_p}, \dot{S}_{e_p}$.  
![](https://i.imgur.com/DFb9zLK.png).  

#### State calculation  
$$
\begin{align}
S &= \dot{e} + ke\\
\dot{S} &= \frac{S(t+\Delta t)-S(t)}{\Delta t}\\
\dot{e} &= \frac{e(t+\Delta t)-e(t)}{\Delta t}
\end{align}
$$  

#### Fuzzy membership function for $S_{e_h}, \dot{S}_{e_h}, S_{e_p}, \dot{S}_{e_p}$  
![](https://i.imgur.com/cjDU6bf.png)  

#### Sliding fuzzy rule   
![](https://i.imgur.com/a4maFRj.png)   

### Action  
1. left motor voltage (feeded to sigmoid function).  
2. right motor voltage (feeded to sigmoid function).  

## Reward  
1. Reward of getting closer.  
    a. If $e_p<1$, then $R_1 = (1-e_p)20$ 
    b. Else $R_1 = -0.02e_p$
3. Move away from goal penalty.  
    a. If $\frac{\Delta e_p}{\Delta t}<-0.01$, then $R_2 = 2$  
    b. Else $R_2=-\frac{1}{200}\frac{\Delta e_p}{\Delta t}$  
5. Correct heading reward.  
    a. If $|e_h|<10$, then $R_3=2(10-|e_h|)$  
    b. Else $R_3=-e_h\frac{1}{100}$
7. Heading away from goal penalty.
    a. If $\frac{\Delta |e_h|}{\Delta t}<-0.01$, then $R_4 = 2\frac{\Delta |e_h|}{\Delta t}$     
    b. Else $R_4=-\frac{1}{200}\frac{\Delta |e_h|}{\Delta t}$  

## Actor Network  
![](https://i.imgur.com/XsUQvLH.png =80x)
![](https://i.imgur.com/kWrKAnz.png =600x)  

## Critic Network  
![](https://i.imgur.com/JHwPkJu.png =150x)
![](https://i.imgur.com/qfM6any.png =500x)  


---

# Result  

## Training result    
The system does not want to learn.  
![](https://i.imgur.com/Aj9Vyh2.png)  

## Target approaching with and without disturbance  
The system failed to a approach point without disturbance.   
![](https://i.imgur.com/sRh7PCk.png)  
![](https://i.imgur.com/ttuSlGt.png)  


## Target approaching with and without disturbance  
NOT YET  

## Following figure of 8  
NOT YET  

## Following figure of 8 under disturbance  
NOT YET    

---

# References

[1]  
[2]  
[3]  
[4]  

###### tags: `fuzzy logic` `matlab` `vrep` `robot` `reinforcement learning`
