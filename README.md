# AI for business 
## Maximizing Revenue of an Online Retail Business
Imagine an Online Retail Business that has million of customers. These customers are only people buying some products on the website from time to time, getting them delivered at home. The business is doing good, but the board of executives has decided to take some action plan to **maximize revenue** even more. This plan consists of offering to the customers the option to subscribe to a premium plan, which will give them some benefits like reduced prices, special deals, etc. 

In this previous utopian example, there are only two strategies, and besides I knew their conversion rates. However in this case study I will be facing 9 different strategies, and my **AI** will have no idea of which is the best one, and absolutely no prior information on any of their conversion rates. However I will make the assumption that each of these 9 strategies does have a fixed conversion rate. These strategies were carefully and smartly elaborated by the marketing team, and each of them has the same goal: convert the maximum clients to the premium plan. However, these 9 strategies are all different. They have different forms, different packages, different ads, and different special deals to convince and persuade the clients to subscribe to the premium plan. Of course, the marketing team has no idea of which of these 9 strategies is the best one. But they want to figure it out as soon as possible, and by **saving the maximum costs**, which one has the highest conversion rate, because they know how finding and deploying that best strategy can significantly maximize the revenues. Also, the marketing experts choose not to send an email to their 100 million customers, because that would be costly and they would risk spamming too many customers. Instead they will subtly look for that **best strategy** through online learning. What is online learning? It will consist of deploying a strategy each time a customer browses the online retail business website to hang out inside or buy some products. Then as the customer navigates the website, he or she will suddenly get a pop-up ad, suggesting him or her to subscribe to the premium plan. And for each customer browsing the website, only one of the 9 strategies will be deployed. Then the user will choose, or not, to take action and subscribe to the premium plan. If the customer subscribes, it is a success, otherwise, it is a failure. The more customers I do this with, the more feed-backs I get, and the better I could get an idea of what is the best strategy. But of course, I will not figure that out manually, visually, or with some simple maths. Instead I want to implement the smartest algorithm that will figure out what is the best strategy in the least amount of time. And that’s for the same two reasons: first because deploying each strategy has a cost (e.g. coming from the pop-up ad), and second because the company wants to annoy the least customers with their ad.

Let's sum up the differences in features of these 9 strategies simply this way:
![alt text](https://imgur.com/yBcebOO.png)

### Simulation ###

In order to simulate this case study, I will assume these startegies have the following conversion rates:

![alt text](https://imgur.com/MKUahit.png)


However, please make sure to understand that in a real life situation I would have no idea of what would be these conversion rates. I only know them here for simulation purposes, just so that I can check in the end that my AI manages to figure out the best strategy, which according to the table above, is strategy number 7 (highest conversion rate).

### Environment to define ###

Online Learning is a special branch of Artificial Intelligence, where there is not much need of defining the states and actions. Here, a state would simply be a specific customer onto whom I deploy a strategy, and the action would simply be the strategy selected. But you will see further in the AI algorithm that I don’t have the states as inputs and the actions as outputs like in my two previous case studies, because this time I am not doing Q-Learning or Deep Q-Learning. Here I am doing online learning. However I do have to define the rewards, since again I will have to make a rewards matrix, where each row corresponds to a user being deployed a strategy, and each column corresponds to one of the 9 strategies. Therefore, since I will actually run this online learning experiment on 10,000 customers, this rewards matrix will have 10,000 rows and 9 columns. Then, each cell will get either a 0 if the customer doesn’t subscribe to the premium plan after being approached by the selected strategy, and a 1 if the customer does subscribe after being approached by the selected strategy. And the values in the cell are exactly, the rewards.
Now a very important thing to understand is that the rewards matrix is only here for the simulation, and in real life I would have no such thing as a rewards matrix. I will just simulate 10,000 customers successively being approached by one of the 9 strategies, and thanks to the rewards matrix I will simulate the decision of the customer to subscribe yes or no to the premium plan. If the cell corresponding to a specific customer and a specific selected strategy has a 1, that will simulate a conversion by the customer to the premium plan, and if the cell has a 0, that will simulate a rejection. Here is below as an example the first rows of a simulated rewards matrix:

![alt text](https://imgur.com/YaXB7ma.png)

According to this simulation, all given in the above rewards matrix:
1. The first customer (row of index 0) would not subscribe to the premium plan after being approached by any strategy.
2. The second customer (row of index 1) would subscribe to the premium plan after being approached by strategy 5 or strategy 7 only.
3. The third customer (row of index 2) would not subscribe to the premium plan after being approached by any strategy.
Thompson Sampling will collect the feed-backs of whether or not each of these customers subscribe to the premium plan one after the other, and thanks to its powerful algorithm, will quickly figure out the strategy with the highest conversion rate, that is the best one to be deployed on the millions of customers, thus maximizing the company’s income from this new revenue stream.

### AI Solution ###

The AI solution that will figure out the best strategy is called "Thompson Sampling". It is by far the best model for that kind of problems in this Online Learning branch of Artificial Intelligence. To recap, each time a new customer connects to the online retail business website, that’s a new round n and I select one among  9 strategies to attempt a conversion (subscription to the premium plan). The goal is to select the best strategy at each round, over many rounds. Here is how Thompson Sampling will do that:

![alt text](https://imgur.com/LCi7B7G.png)

**Intuition.** Each strategy has its own beta distribution. Over the rounds, the beta distribution of the strategy with the highest conversion rate will be progressively shifted to the right, and the beta distributions of the strategies with lower conversion rates will be progressively shifted to the left (Steps 1 and 3). Therefore, because of Step 2, the strategy with the highest conversion rate will be more and more selected.

### Implementation ###

Let’s provide the whole implementation of Thompson Sampling for this specific case study, following the same simulation given above.
While implementing Thompson Sampling, I will also implement the Random Selection algorithm, which will simply select a random strategy at each round. This will be my benchmark to evaluate the performance of the Thompson Sampling model. Of course, Thompson Sampling and the Random Selection algorithm will be competing on the same simulation, that is on the same rewards matrix. And in the end, after the whole simulation is done, I will assess the performance of Thompson Sampling by computing the relative return, defined by the following formula:

![alt text](https://imgur.com/sLVSRzT.png)

I will also plot the histogram of selected ads, just to check that the strategy with the highest conversion rate (Strategy 7) was the one selected the most.


Don’t hesitate to improve the project if you wish with a Pull Request. Until then, enjoy AI for Performance Maximization! 
