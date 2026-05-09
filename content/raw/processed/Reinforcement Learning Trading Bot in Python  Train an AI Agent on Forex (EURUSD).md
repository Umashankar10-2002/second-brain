---
title: "Reinforcement Learning Trading Bot in Python | Train an AI Agent on Forex (EURUSD)"
source: "https://www.youtube.com/watch?v=oW4hgB1vIoY"
author:
  - "[[CodeTrading]]"
published: 2025-12-12
created: 2026-05-08
description: "In this video, we build a reinforcement learning trading bot in Python and train an AI agent on historical EUR/USD Forex data using an hourly timeframe. You’ll see how a model-free reinforcement learn"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=oW4hgB1vIoY)

In this video, we build a reinforcement learning trading bot in Python and train an AI agent on historical EUR/USD Forex data using an hourly timeframe. You’ll see how a model-free reinforcement learning approach allows an AI trading agent to:  
\- Read historical price data  
\- Take long and short trading decisions  
\- Learn from winning and losing trades  
\- Improve its trading policy through rewards  
  
We cover the core reinforcement learning concepts applied to trading:  
Agent, Environment, Actions, Rewards, and Policy.  
  
This is a realistic example of how AI learns trading strategies through trial and error, very similar to how a human trader improves with experience.  
  
⚠️ This video is educational and focuses on algorithmic trading, AI, and reinforcement learning, not financial advice.  
  
○○○ Free Python Script Included, download it below and customize it for your own assets!  
  
╔═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦═╦══╦═╦═╦══╦═╦═╦══╦═╦═╦  
🔗 Resources & Links:  
\--------------------------------------  
• 📚 My Algorithmic Trading Courses → https://codetradingcafe.com  
• 📘 My Book: “Algorithmic Trading with Python” → https://a.co/d/6woMBHt  
• 💻 Free Python Code (GitHub) → https://github.com/ZiadFrancis/ReinforcementTrading\_Part\_1  
  
Happy learning, happy coding ☕  
╚═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩═╩  
  
This educational video focuses on the following topics: reinforcement learning trading, AI trading bot, Forex AI, Python trading bot, reinforcement learning Python, algorithmic trading AI, EURUSD trading strategy, machine learning trading.

## Transcript

**0:00** · Hi and welcome back. This strategy uses reinforcement learning to train a trading AI agent on historical data. I have chosen the URA dollar hourly time frame for today's example. The model showed an increasing equity on learning data and acceptable learning rate. In other words, we're trying to make an AI model that reads historical data, applies trading operations, and learns from winning and losing trades in order to come up with the best trading pattern pretty much like a human would learn trading. You can download the Python code used in this video from the link in the description.

**0:31** · Feel free to explore the files and use them in your own experiments. But first, let's summarize briefly how reinforcement learning works. Reinforcement learning relies on five main concepts. The agent, in this case, it's the one or the model making trading decisions, putting long and short positions, and setting stop-loss and take-profit distances. The environment where the agent operates, the action or the actions that can be taken by the agent.

**0:56** · Then depending on the result of an action, the agent receives a reward that can be either positive or negative with different values. One more concept is the policy which is the agent's strategy or mapping from different states of the environment to actions. In other words, it's the decision patterns learned so far by the agent considering the current environment state. If you are familiar with reinforcement learning, this would be a model-free approach where the agent learns directly from experience or trial and error in the environment.

**1:27** · Think about it as training a dog to complete certain tasks. Every time the dog does well, it will receive a reward. And if it doesn't, then either the reward is null or it can be also negative. Of course, AI agents don't have this intrinsic motivation for the reward. So they can be coded in a way to maximize the reward value. In other words, if the agent receives more reward doing action A, then this action will be attributed the highest probability in the future.

**1:58** · So now we will define our environment, the agent and the list of possible actions that the agent will use to trade in the created environment. And we will let the agent run trading on historical data for around 10 years for example and learning from the reward system the best possible ways of trading just like a human trader learning new strategies and experimenting with trial and error to improve his trading skills. Okay. Now let's see how this is done in Python.

**2:23** · It will be highly technical but you can still follow even if you don't have a purely technical or numerical background because the elements of the code are directly related to trading. I will show you the results and we will discuss how these can be used for our strategies.

**2:39** · Since this project is relatively larger than the previous projects or studies published on this channel. I'm not using a Jupyter notebook file this time. I'm using Python files because we're going to use few files like 1 2 3 four different Python files. So we're splitting the code into four different files in order to make it easier to read and easier to understand. And then we're going to launch it through Python. So we're not using a Jupyter notebook file in this case. However, when you download it, I will be sharing a folder with the data I will be using for this model.

**3:09** · So we can see that we have the Euro US dollar candlestick, the hourly uh data.

**3:17** · It's between 2020 and 2023. And then I have another out of sample data or testing data where I've downloaded between 2023 and 2025. So this is the data on which we're going to test the model after we have trained it on the previous 3 years. I'm going to start with the um indicators.py file. So that's a Python file. I'm using pandas and pandas technical analysis. It's just defining one single function here. Load and pre-process data. It takes a CSV path. So the path for the CSV file.

**3:52** · We're going to read underscore CSV using the path. Clean the data somehow. Sort the index. add some technical indicators, the RSI14, moving average 2050, and the ATR, the moving average 20 slope as well. So that's just the difference between two consecutive rows.

**4:09** · It's not really the regression slope on three or four rows. So it's not really the slope, it's just a difference between uh two consecutive moving average values. And then we're dropping the uh empty values or the empty rows.

**4:23** · We return a data frame with few additional indicators. And this is where if you intend to improve this uh code, this is where we can add some additional indicators and some custom indicators.

**4:35** · Maybe you don't want to use the classic indicators. Maybe you want to add your own. But I mean this is where we can do it. It's in this file. You can define whatever indicators you want uh as functions here and then use them to return the data frame with these indicators. Now we can define the trading environment and this is done using importing gym numpy because we're going to use it for numerical uh analysis or numerical uh operations and from gym we're also importing spaces the observation spaces and the action spaces.

**5:07** · So these are basically uh defining the actions that are allowed uh for for the uh the agent. And I'm defining a class named forex trading environment that inherits from gym.vironment environment class because this is how I want to create the environment by inheriting from the uh package gym. We define the uh constructor. Notice that we have a window size by default equal to 30. So by default the um uh the agent is going to read the last 30 candles before taking a decision.

**5:38** · And this of course includes all the related technical indicators that we've added in the data frame. Now, for the uh stop-loss options, I'm allowing the agent to take one of three decisions. Either 60 pips or 90 pips distance or 120 pips. Where do these come from? These are just random. On the Euro US dollar, I would put uh on the hourly time frame, I would put maybe 60 pips to 90 or 120 pips of stop-loss distance. Same thing for the take-profit options.

**6:10** · So we have 60, 90 and 120. You could add these, you could extend these, but the more options you give to um the agent, the more time it's going to uh take to train the agent and it's going to become computationally more expensive. So it requires more computation time. Now this shouldn't be a problem of course, but for the sake of this video, I kept it as simple as possible to show you how it's done. Now there are three options here for trades.

**6:39** · either the action zero. So it means that we're we're not going to trade. The agent is going to skip the candle without opening any trades. But in the opposite case, if action is positive or it's equal to one, then we have two different directions, either we short the market or the agent will long the market. So either zero or one taking into account of course stop-loss and take profits. We compute the shapes of the data frame to be used later on by the agent. And this is where we initialize the uh current step which is equal to zero at first.

**7:11** · We have the equity $10,000.

**7:15** · Maximum slippage is zero for the moment.

**7:18** · Then we have the uh positions list is empty at this point. And at the end I would like to um plot the equity curve.

**7:26** · So we're going to log the equity curve values and the last trade information.

**7:31** · The function within the class named get observation is simply to return the last window size. Remember that we took 30 by default, 30 rows. So the agent is going to read the last 30 rows but also the number of features. So the shape is going to be window size. It's a numpy array by the way. So it's two-dimensional numpy array with the window size and also accessing all the features available on the data frame.

**7:57** · It also takes care of the edge case at the beginning of the data frame when we don't have enough history. So this is going to be used by the agent to read the data before each candle. And now we have to define the calculate reward.

**8:15** · Remember that the agent is going to behave just like we are training a pet.

**8:19** · Okay, we're training a dog. And we need to provide this reward function to know when we can reward in a positive value or in a negative value the agent. In this case, we're going to use the uh profit and loss for each of the trades.

**8:33** · So, if the agent opens a long position, for example, or any trade and the uh the result of profit and loss is positive, the reward is going to be positive. And it's also proportional to the uh profit and loss value. And that's why at the end of this function, the reward, which is the returned value, is the profit and loss times 10,000 because it has to be adjusted to the uh the number of pips uh from from the Euro US dollar price. In the opposite case, if it's a loss, so if it's negative, in this case, we're going to return a reward that is negative.

**9:07** · Now, since the data is processed in candles, you might have this extreme case where one candle touches the stop-loss and the takerit at the same time. We don't know since we're not using tick data, we don't know which of these uh levels were touched first, were triggered f first. So, we don't know if the trade was a loss or a profit. In this case, just to be on the safe side, we're going to consider it a loss. So we don't cheat our way around.

**9:35** · We're going to in case of a doubt, we're going to consider the trade it's been a loss and we're going to uh return a negative reward as well. And that's it basically.

**9:47** · Now we still have to define one more function that's uh the step function.

**9:52** · It's going to consider all of the previous uh functions. So we have direction, stop-loss, and a takerit and a reward and so on. It's going to crunch it all together. and it's going to return the observation, the reward and other information. The reset function resets the uh the values of the back test. So, uh to the current step and the equity 10,000 and uh it empties the equity curve list and so on to uh to restart the test actually. Then we can render the equity curve using the render function.

**10:22** · So that was our trading environment.py. Now to train the agent, we're going to use all of these functions and classes to make it happen.

**10:32** · So we're going to import from stable baseline 3 the PO. That's the um the model we're going to use to train the agent. And if again if you are coming from data science AI or reinforcement learning and you are a bit familiar with these, this is a model free approach.

**10:50** · This means that the agent is going to learn directly from the environment. We don't have the whole environment map in front of us and we're asking the agent to learn from the map. It's actually going to interact step by step with the candles with the historical data trial and error and it's going to adjust the parameters uh when it's progressing through the data. So first we're going to load and process the data. I have the euro US dollar hourly time frame 2020 2023. I'm creating actually an environment.

**11:18** · So using the uh the class forex trading environment providing the data frame the window size of 30 the stop-loss options which you can change here the take-profit options then we have a dummy vector declaration that is required by stable baselines for parallelization so we're not going to uh go into the technical details but this is where you can also experiment to change the po now I'm not saying that you will be getting better results it's just that for learning purposes and for educational purposes.

**11:50** · It's good also to train the model using different models or uh the agent actually train the agent using different models. The PO is actually one of the best suited models for uh for this case for financial trading uh simply because this is a very noisy and continuous data. So we assume that the data is flowing continuously.

**12:14** · you the agent is going to receive data live from the market and it will build its skills trading live on the market checking whenever we have a loss whenever we have a winning trade and so on so it's kind of acquiring this experience and in this case PO works

**12:30** · well then we're going to train the model so using modelarn the total total time steps actually is 50,000 you might want to adjust this one as well if you increase it it's going to uh train the model more in a better way but it's requires also it requires also

**12:47** · uh additional computational power then we can save the model as model euras dollar and that's the zip file you can see here I've already run and trained the model and I've saved it here for later to be used and uh at the end we print model saved successfully then we can evaluate or test the model so we're going to um reset the environment uh the equity curve is empty again and then we're going to try to predict use the model to predict values using the observation space. We don't have any stochastic uh operations included.

**13:17** · So that's deterministic and for each um step we're going to apply the action buying or selling and so on. We're going to record the observation, the reward and if it's done or not. So if it's finished or not and some additional information and at the end I'm going to append the equity uh with the current equity actually. So that's going to build our equity curve.

**13:43** · Uh so we're going to append all the equity values or the balance values in the equity curve list to be able to plot it using this part of uh of the file. To be able to run this, I will be opening a new terminal. I'm going to um source my environment because I've created a virtual environment specifically for this application. Virtual environment scripts activate. I'm going to run python train uh agent.py. pi and I'm going to run it. So, it's going to take a while before it finishes.

**14:15** · So, as you can see, you can follow up what's happening, the uh elapse time, the learning rate, the loss value. And once this is done, it's going to plot the equity curve on the training data. And as you can see, it's training well. So it's managing to increase uh the equity which means that basically the agent knows uh that it needs to follow the positive rewards action or course of actions.

**14:42** · So it's building a kind of policy that will allow the equity to increase uh over time with it with the different trades. Now the correct way to evaluate the agent is actually to test it on new and unseen data. This is the training data and it's working well. We can see that the equity is positive. the agent is heading in the correct direction. Let's close this one and head to the test agent.py file. And here I'm loading a new unseen data. So that's always the uras dollar candlesticks 1 hour uh time frame.

**15:13** · But this time it's 2023 up to 2025. I'm not going to train the model here. It's not going to fit or apply any fitting. It's just going to try and trade. But I'm still using the same options for stop-loss and take profits. The same window size as what we have used for the training part. And I'm going to run this uh same model. So we're loading the model that we have saved from the uh training phase or the learning phase.

**15:41** · And we're going to try and test the agent. So python test agent.py.

**15:51** · It also takes a bit of time before showing the equity curve. And this is what we're getting. So it's not what we've expected. The equity was showing a more positive trend using the training steps or the training data. But this is on new and unseen data. It's not very bad either because to be honest we didn't provide much for the um uh for the agent. So these are barely few technical indicators.

**16:16** · These are classic technical indicators. the two moving averages, the RSI, the ATR, and what we're calling a slope, which is not really a slope. We didn't apply aggression. This is just to show you an example as simple as possible actually just for the sake of this video. But in this function, you might want to think how you can add additional technical indicators that matter for the trading that matter for the agent that can provide additional and valuable information for the agent to learn how to trade.

**16:47** · One thing also that we could be changing in the trading environment these options. So I've also provided very limited options for the stop- loss and take profit values. So it's either 6090 or 120 pips for both. Maybe this is not enough for trading the Euro US dollar. maybe we should be providing more values maybe with five pips of increments uh covering from 30 pips up to I would say 100 pips for example for

**17:16** · both stop-loss and take profit options so that's one thing to be uh to be improved also when we were training the agent we used 50,000 time steps maybe the agent is overfitting we could try to um fit it with 10,000 steps for example so now if I'm interrupting ing and retraining with 10,000 steps. I'm going to show you, let me save it first. So, I'm going to show you the uh effect of this small uh parameter.

**17:46** · So, I just switched from 50,000 time steps of training down to 10,000 time steps. And this is the training equity again. It's working well. Now, we can test the model. The equity that we're going to get is slightly different. So as you can see it's kind of positive at first, it's not as positive later on and so on.

**18:07** · So sometimes you might get the set of parameters that will allow you to um train the model but then test it also on unseen data and you can still have this positive equity trend uh even when you are testing on unseen data. So as you may have noticed there's a lot of options that we can still use to improve the trading agent uh potential. I still find it enjoyable to be honest.

**18:31** · Uh adding some more stop-loss options, take profit options and trading indicators, maybe the classic or custom indicators and so on. Changing the total time steps uh in order to avoid overfitting the model on the training data and so on.

**18:49** · So, it's a lot of fun and seeing the results straight in front of us is also powerful because you can see the effects immediately in front of you. And that will be it for this video. I hope you guys liked it and found the information helpful. I've been receiving lots of requests recently. Why don't we use the reinforcement learning in trading? As you may have noticed, it's very powerful. It has a lot of potential, but it's not as simple to fine-tune as well because you have a lot of noise in the trading data.

**19:16** · So this is the nature of the market and sometimes the model is finding it difficult to pick up the signal the true signal of the trend from all the noise that you can find in the data. But anyway I hope you guys liked it. I hope you found this information helpful. If so please leave a like, leave a comment, drop your ideas in the comments section. This was requested by one of the uh viewers through the comment section. So don't hesitate to drop us some of your ideas. Thank you so much for watching. Thank you so much for staying that long.

**19:48** · Until our next one, trade safe and see you next time.