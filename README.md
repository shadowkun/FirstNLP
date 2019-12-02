# FirstNLP
Try NLP with me.
使用NLTK找出所有的语法解析树

使用NLTK完成Udacity公开课CS271（Intro to Artificial Intelligence）的Final Assessment Question 20


首先我们按照题目要求编写语法规则final_question_20.fcfg
```
           % start S
           S[SEM=(?np + ?vp)] -> NP[SEM=?np] VP[SEM=?vp]
           S[SEM=(?s1 + and + ?s2)] -> S[SEM=?s1] 'and' S[SEM=?s2]
           NP[SEM=?n] -> N[SEM=?n]
           NP[SEM=(?d + ?n)] -> D[SEM=?d] N[SEM=?n]
           NP[SEM=(?adj + ?n)] -> ADJ[SEM=?adj] N[SEM=?n]
           NP[SEM=(?d + ?adj + ?n)] -> D[SEM=?d] ADJ[SEM=?adj] N[SEM=?n]
           VP[SEM=(?v + ?np)] -> V[SEM=?v] NP[SEM=?np]
           VP[SEM=?v] -> V[SEM=?v]
           VP[SEM=(?v + ?np + ?np)] -> V[SEM=?v] NP[SEM=?np] NP[SEM=?np]
           N[SEM='fall'] -> 'fall'
           N[SEM='spring'] -> 'spring'
           N[SEM='leaves'] -> 'leaves'
           N[SEM='dog'] -> 'dog'
           N[SEM='cat'] -> 'cat'
           V[SEM='spring'] -> 'spring'
           V[SEM='leaves'] -> 'leaves'
           V[SEM='fall'] -> 'fall'
           V[SEM='left'] -> 'left'
           D[SEM='the'] -> 'the'
           ADJ[SEM='fall'] -> 'fall'
           ADJ[SEM='spring'] -> 'spring'
           ADJ[SEM='purple'] -> 'purple'
           ADJ[SEM='left'] -> 'left'
```

然后使用nltk对这些句子进行语法树解析，打印最终语法树列表的长度即可：
```
           from nltk import load_parser
           sentences=['fall leaves fall',
                      'fall leaves fall and spring leaves spring',
                      'the fall leaves left',
                      'the purple dog left',
                      'the dog and cat left']
           cfg_path='../grammars/cs271/final_question_20.fcfg'
           parser=load_parser(cfg_path)

           for sentence in sentences:
               trees= list(parser.parse(sentence.split()))
               print('%s:%s'%(sentence, trees.__len__()))
```

其输出如下：

```
           fall leaves fall:2
           fall leaves fall and spring leaves spring:4
           the fall leaves left:1
           the purple dog left:1
           the dog and cat left:0
```

当然我们还可以打印出每一棵语法树

```
     i=1
     for tree in trees:
         print('tree_%s:'%i)
         print(tree)
         i+=1
```
