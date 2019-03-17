                                            VC theory---Hoeffding’s Inequality
Abstract: Hoeffding’s inequality provides an upper bound on the probability that the sum of bounded independent random variables deviates from its expected value by more than a certain amount. In this part, we will see the theorem and proof of Hoeffding’s inequality and how we use this theorem to estimate the relationship between Ein and Eout  in binary case.

Key Words: Hoeffding inequality, in-sample error, out-of-sample error

Theorem: Let Z1,…Zn be independent bounded random variables with Zi ∈[a,b] for all i, where -∞﹤a≤b﹤∞,i=1,…,N. Then             P(1n ∑(Zi-E[Zi])>t) ≤exp(- 2nt2(b-a)2 )         for all t≥0.

Proof: Let Z =1n ∑(Zi-E[Zi]).Since the left part of this equation is the form of 
                              Pz( f(Z))> t
, which we can change it by indicator function, then
                              Pz( f(Z)>t)=EZ[1{ f(Z)-t>0}], 
since this indicator function can be bouned by an exponential function (as the figure below shows), then
                              Pz( f(Z)>t) ≤ EZ[exp(η( f(Z)-t))], 
where η is an any positive number.
 
Then we can get: P(1n ∑(Zi-E[Zi]) >t)=P(nZ -nE[Z ]>nt)
                                     ≤E[exp(η(nZ -nE[Z ]-nt))]
                                     =e-nηt∏E[exp(η(Zi-E[Zi]))]
Then 
E[exp(η(Zi-E[Zi]))]=e-ηEZi E[exp(ηZi)]       
                   ≤e-ηEZi (b-EZib-a * eηa +EZi-ab-a * eηb) 
                   = e-η(EZi-a)(1-EZi-ab-a +EZi-ab-a * eη(b-a))
                   =exp(-η(b-a)pi)*exp log(1-pi+pi eη(b-a))
                   =exp(-ηipi+log(1-pi+pi eηi)) 
,where pi=EZi-ab-a , ηi=η(b-a), let L(ηi)= -ηipi+log(1-pi+pieηi) ,
Then   L’ (ηi)= -pi+pieηi 1-pi+pieηi  = - pi+   pi (1- pi) e-ηi+ pi     
     L’’ (ηi)=pi(1- pi)e-ηi/[(1-pi)e-ηi+pi]2
             ≤ 14  [(1- pi)e-ηi+pi]2 [(1- pi)e-ηi+pi]2  =14 
Take Taylor expansion at 0, then 
             L(ηi)=L(0)+L’(0) ηi+12 *L’’(ζ)ηi2
                  ≤L(0)+L’(0) ηi+18 * ηi2
                  =18 * η2(b-a)2
Then  E[exp(η(Zi-E[Zi]))] ≤eL(ηi) ≤e^18 * η^2(b-a)^2 
Then   P(Z -E[Z ]>t) ≤e-nηt∏e^18 * η^2(b-a)^2 
=exp(n8 * η2(b-a)2-nηt)
For any η>0, the equation holds, since the minimum value of the right side is η=4t/(b-a)2>0, then we will get
P(Z -E[Z ]>t) ≤exp(- 2nt2(b-a)2 )
, which proves the Hoeffding equation holds.

Special case of Binary classification:
Let X be input space, Y={+1,-1} be output space, there is an unknown distribution PXY on X×Y, a hypothesis space H, a loss function l:H×X×Y→R+, there are also n independent randpm variables chosen from PXY. We want to get a hypothesis g∈H, which makes the out-of-sample error small enough, where 
Eout(g)=EPxy [l(g,X,Y)]
And in binary classification, we define loss function as binary error, which is l(h,x,y)=1 if h(x) ≠y .
Based on the randomness of training sample{(xi,yi)}, there will be probability which is no less than 1-δ that satisfiies the equation:
                                                  Eout≤Ein+Ω
, where Ein(g)=1n ∑l(g,xi,yi) .
For a fixed h, according to the Hoffding’s inequality theorem, since binary loss only has two values which are 0 and 1, then a=0,b=1 .
Then we can get      P(Ein-Eout>t) ≤exp(-2nt2)
Or                   P(|Ein-Eout|>t) ≤2exp(-2nt2)
Then                 P(|Ein-Eout|>t)= P(Ein-Eout>t)+ P(Ein-Eout<-t)
                                    = P(Ein-Eout>t)+ P(-Ein+Eout>t)
Then we can get  t= (log1 δ 2n )^12 
Thus there is probability which is no less than 1-δ that satisfiies the equation:           Eout≤Ein+ (log1 δ 2n )^12 

References: 
1.Wikipedia, https://en.wikipedia.org/wiki/Hoeffding%27s_inequality
2. http://freemind.pluskid.org/slt/vc-theory-hoeffding-inequality/
3.John Duchi, CS229 Supplemental Lecture notes Hoeffding’s inequality, http://cs229.stanford.edu/extra-notes/hoeffding.pdf
4.Hoeffding.W(1963).Probability Inequalities for Sums of Bounded Random Variables, Journal of the American Statistical Association,58(301),13-30
