---
title: "OpenAI-Gym for Reinforcement Learning"
date: 2018-03-13 12:26:28 -0400
categories: Reinforcementlearning update
use_math : true
---




# 강화학습과 친해지기 위한 OpenAI의 Gym사용법

강화학습을 공부해보신 분들은 Gym이라는 용어를 많이 들어보셨을 것이다. 

체육관의 의미를 가진 Gym은 무엇이며, 강화학습에 어떻게 사용될까?



먼저 Gym은 OpenAI라는 회사에서 만들었다.

Gym을 만든 OpenAI는 비영리 인공지능 연구소이며, 안전한 인공지능을 만드는 것이 목표라고 한다. 


OpenAI는 Gym과 Baselines라는 라이브러리를 제공한다. 

Gym은 Reinforcement Learning Algorithms을 개발하고 비교하기 위한 툴킷 이고,

algorithm을 실험해 볼 수 있도록 여러가지 Environments을 제공한다. 	


[Gym 환경모음 링크](http://gym.openai.com)

[Gym  webistie 링크](http://GYM.OPENAI.COM)

Baselines는 강화학습 알고리즘 모음이다. 

OpenAI는 강화학습을 실험해볼 수 있도록, gym과 Baselines같은 강화학습 환경과 알고리즘을 제공한다. 



[Baselines 깃허브 링크](https://github.com/openai/baselines)


### 1. gym 설치하기
`pip3 install gym`

gym을 설치하기 위해 python 3.5이상 버전에서 pip3 명령어로 gym을 설치한다. 

또는

git clone을 하여 설치한다. 

```
git clone https://github.com/openai/gym
cd gym
pip3 install -e .
```

- - -

### 2. Environments

Algorithm을 환경에 적용해 보기전에, 

Cartpole이란 게임을 gym라이브러리를 통해 불러와서 action을 선택해보도록 하겠다. 

a. 함수 설명

`gym.make()` : 강화학습 환경을 불러온다.  

`env.reset()` : 환경을 초기화 한다. 

`env.render()` : 화면을 출력한다.

`env.action_space.sample()` : 임의의 action을 선택 

`env.step` : 선택한 action을 환경으로 보낸다.

```
import gym

env=gym.make('CartPole-V0')

env.reset()

for i in range(1000):
	env.render()
    	env.step(env.action_space.sample())

```

위와같은 python코드로, 

gym을 통하여 카트폴 환경을 부르고, action을 선택하며 화면에 표시를 할수 있다.

다른 환경을 불러오기를 원하면 `gym.make('CartPole-V0')` 대신에 [Gym 환경모음 링크](http://gym.openai.com) 에서 원하시는 환경을 선택하면 된다.

- - -

### 3. Observations

위의 예는 env.action_space.sample()을 통하여 임의의 action을 선택하였다.

이렇게 임의의 action을 선택하지 않고 더 좋은 action을 선택하려면, 

우리가 선택한 action이 환경에 어떻게 작용하는지 알면 좋을것이다. 

이 기능한 하는 함수는 위에서 본 `step`함수이다. 

이 선택한 action을 `step`함수로 보내면, 다음의 4가지 value를 return한다. 

* observation : 픽셀 데이터과 같은 관찰값

* reward : 그 action을 하므로서 환경에서 받는 reward값

* done : 에피소드가 terminal 되면 True( 목표를 달성했거나, 에이전트가 목숨을 잃었을때)

* info : 환경의 정보들( 점수 등등 ) 


Agent는 각 time step마다 action을 선택하며 Environment과 상호작용을 한다. 

이때 Environment는 Agent로부터 action을 받고 reward와 observation을 return 한다.

```
import gym
env=gym.make('CartPole-v0')

for i in range(20):
	observation=env.reset()
    for t in range(100):
    	env.render()
        print(observation)
        action= env.action_space.sample()
        observation, reward, done, info = env.step(action)
        
        if done:
        	print("{} timestep 뒤에 에피소드가 끝났습니다.".format(t+1))
            break
```
 
 

강화학습을 실험하며, 꼭 알아야할 OpenAI의 gym 함수 사용법에 대하여 간단하게 알아보았다. 

더 자세한 환경 설치법과 설명은 [Gym 깃허브 링크](http://github.com/oepnai/gym)에서 구현된

코드를 공부하면 좋을것 같다. 



Reference 

* https://openai.com


