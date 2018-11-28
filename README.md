# Yelp-User-Review-Analysis-Using-K-Means++
For faster initialization of the centroids the algorithm selected must approximate the posterior distribution of the dataset with very few passes over the data. Some of the algorithms which give good approximation of the distribution are the random walk Monte Carlo algorithms(Metropolis–Hastings algorithm, Gibbs Sampling, etc). These algorithms make use of the markov chains algorithm for a quick and efficient approximation.<br />
Hence, implementing an algorithm which makes use of markov chain would give us the best results<br />
We would like to approximate the probability distribution of our data by constructing a sequence of markov chains and passing through them<br />
<br />
## Algorithm:
1) Initialize an arbitrary centroid which lies on the data at random<br />
2) Compute the probability distribution of all the data points with reference to the assigned centroid<br />
3) Pick a point at random  from the data set to start the markov chain. This point will act as the initial state in our sequence of        
   points<br />
4) Sample the next state form the dataset based on the probability distribution. Compute the probabilities of staying in the same 
   state and moving to the next state<br />
5) Depending on the probabilities move to the desired state by introducing randomness in the decision<br />
## Our Contribution:
### Probability of State change:<br />
1) The state change or stay probability is computed by taking the sign of the distance between the present and future states to 
   their respective centroids<br />
   dist (xj+1- xj) = D(xj+1,C) – D(xj,C)<br />
   where D(x, C) is the distance square of the point x from the known centroid set C<br />
2) This gives a good estimation of movement in markov chains to different chains at time ‘t’. The estimation is similar to the    
   Metropolis Hashing technique and gives similar results<br />
3) By comparing the difference between the distances and taking the sign we can say which state is farther to the centroid based on    
   the sign value. The new state will be assigned based on the sign value which gives a good approximation of the distances to the  
   centroids<br />
4) The points with huge distances and with negative sign are mapped with the function e^x. This maps (-inf, 0] to [0,1] 
### Update Rule
1) The difference is computed between the next state and the current state in that order. If the distance is positive, it means the next state is farther to the centroids than the current state. Hence, we move to the next state<br />
2) If the distance is negative the current state is farther than the next state. Hence, we stay in the same state. The distance 
   here is mapped from (-inf, 0] to [0,1]. We then sample from uniform distribution to decide the change in state based on the 
   mapped distance values<br />
   p(xj+1/xj) =  exp(dist(xj+1- xj))<br />
3) If the sampled uniform probability is less than the mapped distance, we move to the next state else we stay in the same state
<br />
The graph shows how the distances are mapped after passing the function e^x

## Results:
![markov2](https://user-images.githubusercontent.com/41950483/49135046-948aeb00-f2b3-11e8-8e7f-a557d8e0f407.png)<br />
The algorithm proposed is much faster than Kmeans++ seeding since we approximate the probability distribution with just a few passes over the data for each centroid. 
The proposed method which uses markov chain approximation takes 42 seconds with a batch of 500 data points to converge. For the same batch value, Kmeans++ initialization takes 218 seconds. This difference is largely due to the initialization of the centroids





