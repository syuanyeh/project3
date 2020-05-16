---
date: "2020-05-14"
highlight: "true"
linktitle: Using R and Python together for statistic tests
title: Using R and Python together for statistic tests
---

## randomization test!
although I have only come to know python this semester, I have already found some convient way to incorporate python codes into my lab data analysis. I have always stick to R studio for data analysis, yet the fast and more straight input of python code for certain statistical test is just too temping for a lazy person like me.
For instance, In my attempt to analyze my collected swordfish mating behaviors data in the lab, I ran a randomization test on my data as my data failed the ANOVA assumptions. the coding look something like this:

    ▾ ```{r}
      obs_F<- 7.931 
      Fs<-replicate(5000,{
      new<-Data%>%mutate(Counts=sample(Counts)) 
      SSW <- new%>%group_by(Behaviors)%>%summarize(SSW=sum((Counts-mean(Counts))^2))%>%
      summarize(sum(SSW))%>%pull
      SSB<- new%>%mutate(mean=mean(Counts))%>%group_by(Behaviors)%>%mutate(groupmean=mean(Counts       ))%>%
      summarize(SSB=sum((mean-groupmean)^2))%>%summarize(sum(SSB))%>%pull
      (SSB/9)/(SSW/152)
      })
      hist(Fs, prob=T); abline(v = obs_F, col="red",add=T)
      mean(Fs>obs_F)
      ```
I had to double checked and proofread my code from my comp bio lecture slides before it actually works (I am very bad at coding. If you can't figure that out by looking at my website, bless your soul!) the language of R can be tough on a amateur like me. 

last week, I discovered doing randomization test in python(after defining the dataset as data and the true mean difference between group as true_diff) look something like this:

    ▾mean_diff=np.empty(5000)
    for i in range(5000):
        data['bodysize']=np.random.permutation(data['bodysize'])
        mean_diff[i]=data[data.bodysize=="large"].Courtship.mean()-data[data.bodysize=="small"].         Courtship.mean()
    np.mean(mean_diffs>true_diff)
    
Both randomization test gived me a p vlaue close to zero. Not only is python code shorter(No SSB or SSW calculation needed), the coding language also looks a lot more straightfoward for a rookie like myself. 

## Back to ANOVA
after checking the result with randomization test, I had to go back and use ANOVA on the data (professor asked for ANOVA), and this is when I realized doing ANOVA in R is a LOT easier in R than in python.
all I did for ANOVA and posthoc t tests in R:

    ▾```{r}
    summary(aov(Counts~Behaviors, data=Data))
    pairwise.t.test(Data$Counts, Data$Behaviors, p.adj = "none")
     ```
I then, out of curiosity, went to the lecture slide to look for code for ANOVA in python, think that I might again find simpler coding from python, and this is what I found:

    ▾import seaborn as sns
    import statsmodels.api as sm
    from statsmodels.formula.api import ols
    Data= sns.load_dataset('mating_counts')
    fit = ols("Court_counts~C(bodysize)",data=Data).fit()
    anova_table = sm.stats.anova_lm(fit,typ=2)
    anova_table
all the importing is already bad enough for somone that hate extensive typing, the posthoc test is even worse as I can not understand the logic behind the coding!

I end up submitting the python codes for my randomization tests and R studio code for my ANOVA to my professor to minimize the words I had to type for my data analysis report (this end up backfire as my professor only take R code or excel code so I had to resubmit my R code for randomization test). 
## Moral of the story: 
1. both python and R had its strength in the coding of certain statistic tests and using them together seem to be the most efficient way to analyze data. 
2. Don't be as lazy as I was :) 


