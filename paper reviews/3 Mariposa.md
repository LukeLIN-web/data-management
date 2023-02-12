

| Reviewer **(R2)**                                 |
| ------------------------------------------------- |
| Mariposa: a wide-area distributed database system |
| UCB                                               |
| CS  341                                           |

## Summary 

- A distributed microeconomic approach is presented for managing query execution and storage management.
- Mariposa is a flexible and powerful approach for distributed data management, with an economic model reducing complexity and a bidding protocol that is not too expensive.
- The authors plan to release a general version of Mariposa by the end of 1995.

## Strengths

1. A flexible and powerful approach for WAN environments.
2. The economic model reduces the complexity of scheduling through "invisible hand" guidance for equitable resource trading.
3. Bidding protocol results in flexible execution plans that can adapt to changing environments and unbalanced workloads.

## Weaknesses

1. Lack of graphical representation to illustrate experimental results.
2. Important points are not emphasized in the table. We don't really know what the main improvement is.
3. The system is a combination of old and new code. But a comparison with the previous system is missing, leading to uncertainty about whether the new system is an improvement. Maybe the old system has a similar performance to the new system because there are too many different factors.

## Justification

1. Chapter 3 clearly justifies how the network bidder makes full use of bandwidth.
2. This paper develops a decentralized naming facility that does not depend on a centralized authority for name registration or binding so that it has good scalability.
3. Since maintaining synchronization between the various components of a distributed system can be difficult and resource-intensive. This system does not force a site to synchronize with all other sites.
4. The experiments demonstrate the power, performance, and flexibility of the Mariposa approach to distributed data management.

postgres.

目前的系统3个假设,

1.  static data allocation . 
2. single 管理员
3. uniformity 

所以不适合分布式.

没有全局同步. 但是不代表没有全局consistency. 

name server 存储metadata?  

现在很多论文还是用这个想法.

