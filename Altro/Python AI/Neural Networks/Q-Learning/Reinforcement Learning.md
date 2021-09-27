- This technique is different than many of the other machine learning techniques we have seen earlier
	-  Rather than feeding our machine learning model millions of examples we let our model come up with its own examples by exploring an enviornemt
		-   Humans learn by exploring and learning from mistakes and past experiences so let's have our computer do the same

## Terminology
- **Enviornemt** This is what our _agent_ will explore. 
	- An example of an enviornment in the case of training an AI to play say a game of mario would be the level we are training the agent on.

- **Agent** an agent is an entity that is exploring the enviornment. Our agent will interact and take different actions within the enviornment.
	-  In our mario example the mario character within the game would be our agent.

- **State** always our agent will be in what we call a _state_. The state simply tells us about the status of the agent. The most common example of a state is the location of the agent within the enviornment. Moving locations would change the agents state.

- **Action** any interaction between the agent and enviornment would be considered an action. 
	- For example, moving to the left or jumping would be an action. An action may or may not change the current _state_ of the agent. In fact, the act of doing nothing is an action as well! The action of say not pressing a key if we are using our mario example.

- **Reward** every action that our agent takes will result in a reward of some magnitude (positive or negative). The goal of our agent will be to maximize its reward in an enviornment. Sometimes the reward will be clear, for example if an agent performs an action which increases their score in the enviornment we could say they've recieved a positive reward. If the agent were to perform an action which results in them losing score or possibly dying in the enviornment then they would recieve a negative reward.

- The most important part of reinforcement learning is determing how to reward the agent. The goal of the agent is to maximize its rewards. 
	 - This means we should reward the agent appropiatly such that it reaches the desired goal.

[[Q-Learning]]