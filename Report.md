## Implmentation and Algorithm

We train the agent using a DDPG as introduced in [CONTINUOUS CONTROL WITH DEEP REINFORCEMENT
LEARNING](https://arxiv.org/pdf/1509.02971.pdf). Some hyper parameters used in training:

 actor_fc1_units=100, actor_fc2_units=100, critic_fc1_units=100, critic_fc2_units=100,
              lr_actor=1e-5, lr_critic=1e-4, buffer_size=int(1e6)
buffer_size=int(1e5), 
                 batch_size=128, gamma=0.99, tau=1e-3, lr_actor=1e-4, lr_critic=1e-3, 
                 weight_decay=0, actor_fc1_units=400, actor_fc2_units=300              
Actor Learning Rate: 1e-5
Critic Learning Rate: 1e-4
Replay Memory Buffer Size: 1e6
Batch Size: 128
Gamma (belman equation discount factor): 0.99
Tau (soft update of target network's parameters): 1e-3

In particular, I found that slowing down the learning rate from 1e-4 to 1e-5 and 1e-3 to 1e-4 respectively led to more stable learning.

More importantly, increasing the replay memory buffer size from 1e5 to 1e6 gave he agnet the memory to go from an average score of ~2 to ~30.

## Neural Net Model

### Actor
Input layer: 33 units
Hidden Layer w/ Relu 1: 100 units
Hidden Layer w/ Relu 2: 100 units
Output layer (tanh): 4 units

### Critic
Input layer: 33 units
Hidden Layer w/ Relu 1: 100 units
Hidden Layer w/ Relu 2: 100 units
Output Layer: 1

Each layer is fully connected with RELU activation.

## Episodes

It required approximately 3500 episodes to train the agent and achieve an average score of 30+ over 100 episodes. I am unable to present the entire progress here because the environment in which I ran the training crashes every 700-1200 episodes.

As such, I had to resume training from existing checkpoints. Note that the actor / critic's local network and target networks resumed to the same checkpoints, even if the local / network weights were not the same when the previous session terminated.

The snippet below is from the final training session. The score starts high at 11.80 because we resumed from previous a checkpoint that had already trained for ~2700 episodes.

Episode 50	Average Score: 11.80
Episode 100	Average Score: 14.25
Episode 150	Average Score: 15.15
Episode 200	Average Score: 17.17
Episode 250	Average Score: 19.25
Episode 300	Average Score: 20.04
Episode 350	Average Score: 19.76
Episode 400	Average Score: 20.58
Episode 450	Average Score: 22.79
Episode 500	Average Score: 25.18
Episode 550	Average Score: 24.40
Episode 600	Average Score: 26.18
Episode 650	Average Score: 30.12
Episode 700	Average Score: 33.36
Episode 750	Average Score: 33.27
Episode 775	Average Score: 33.84


## Future Work
I suspect tweaking increasing the learning rate can speed up learning by 2x-3x.