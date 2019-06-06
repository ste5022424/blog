---
title: Linq Join Lambda expression
date: 2019-04-18 18:06:29
categories:
- Linq
tags:
- Linq
- C#
---

# Linq Join Lambda expression

> [Eaxlample](https://github.com/ste5022424/Linq_Join_Lambda_Expression.git)

```C#

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp20
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var memberdata = new List<Member>()
            {
                new Member(){ MemberID = 1, MemberAccount = "小明"},
                new Member(){ MemberID = 2, MemberAccount = "小王"},
                new Member(){ MemberID = 3, MemberAccount = "小華"},
            };

            var scoredata = new List<Score>()
            {
                new Score(){ MemberID = 1, score = 100},
                new Score(){ MemberID = 2, score = 50},
                new Score(){ MemberID = 3, score = 40},
            };

            var membergamelogdata = new List<MemberGameLog>()
            {
                new MemberGameLog() { MemberID = 1 , LogID = 4001 , LogName = "打棒球" },
                new MemberGameLog() { MemberID = 2 , LogID = 4002 , LogName = "打羽球" },
                new MemberGameLog() { MemberID = 3 , LogID = 4003 , LogName = "打籃球" }
            };

            var joindata = memberdata
                            .Join(membergamelogdata,
                            member => member.MemberID,
                            gamelogdata => gamelogdata.MemberID,
                            (member, gamelogdata) =>
                            new
                            {
                                MemberID = member.MemberID,
                                MemberAccount = member.MemberAccount,
                                LogID = gamelogdata.LogID,
                                LogName = gamelogdata.LogName
                            })
                            .Join(scoredata,
                            memberjoin1 => memberjoin1.MemberID,
                            score => score.MemberID, (memberjoin1, thescore) =>
                            {
                                // Declare variable within LINQ select
                                var getscorestring = getScoreString(thescore.score);
                                return new
                                {
                                    MemberID = memberjoin1.MemberID,
                                    MemberAccount = memberjoin1.MemberAccount,
                                    score = getscorestring,
                                    LogID = memberjoin1.LogID,
                                    LogName = memberjoin1.LogName
                                };
                            });

            foreach (var item in joindata)
            {
                Console.WriteLine($"{item.MemberID}, {item.MemberAccount}, {item.score}, {item.LogID}, {item.LogName}");
            }
        }

        private static string getScoreString(int score)
        {
            if (score > 80)
            {
                return "甲";
            }
            else if (score > 60)
            {
                return "乙";
            }
            else
            {
                return "丙";
            }
        }

        private class Score
        {
            public int MemberID { get; set; }
            public int score { get; set; }
        }

        private class Member
        {
            public int MemberID { get; set; }

            public string MemberAccount { get; set; }
        }

        private class MemberGameLog
        {
            public int MemberID { get; set; }

            public int LogID { get; set; }
            public string LogName { get; set; }
        }
    }
}

```

![](https://i.imgur.com/iE0Zy2O.png)


# 參考

[Linq Join & Lambda Join](https://dotblogs.com.tw/erictsaiblog/2015/05/17/151321)
[How to rewrite this LINQ using join with lambda expressions?](https://stackoverflow.com/questions/13692015/how-to-rewrite-this-linq-using-join-with-lambda-expressions)
[How to join 3 tables with lambda expression?](https://stackoverflow.com/questions/9120088/how-to-join-3-tables-with-lambda-expression)
[Declare variable within LINQ select](https://stackoverflow.com/questions/29251075/declare-variable-within-linq-selectx-new)