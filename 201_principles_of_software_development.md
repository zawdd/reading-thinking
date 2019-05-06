# 软件开发的201条准则
# 201 principles of software development
## Chapter 1 介绍
软件工程需要有别于物理，生物等工程的原则。
原则原理-》技术-》语言-》工具
原则在发展和变化，适用于以前的不一定适合现在。
## Chapter 2 通用原则
### principle 1: Quality is #1
>A customer will not tolerate a product with poor quality, regardless of the definition of quality. Quality must be quantified and mechanisms put into place to motivate and reward its achievement. It may seem politically correct to deliver a product on time, even though its quality is poor, but it is politically correct in the short term only; it is political suicide in the middle and long term. There is no trade-off to be made. The first requirement must be quality. Edward Yourdon suggests that you Just say no”when you’re asked to speed up testing, ignore a few bugs, or code before agreeing on a design or a set of requirements

#### 质量是第一位的
即使短期内看，按时上线是政治正确的，但是其牺牲了中长期了利益。对于质量没有什么可权衡了，必须要保证。应该把质量保证做如激励和奖励的机制中去。要say no，当需要跳过测试，忽略bug，在有完整的设计前就开始开发时。
#### 思考
**首先，要区分什么是质量问题，为了快速迭代，原型的开发去掉了一些功能，等并不是质量问题。其次，软件中的bug是不可避免的，我们要解决我们发现的问题，但是没发现的问题我们也解决不了，不能认为我们按照了质量工程流程的要求做了该做的，就没有质量问题了，依然要准备好出了质量问题的预案。最后，如果我认为质量还是会有trade off的，如果保证质量的代价，大于出了质量问题的代价，那么或许就不值得了，比如密码学中不需要绝对的安全，只需要破解的代价足够大就可以了，当然现实时间的代价，不是计算机中的时间复杂度那样可以明确量化衡量的，有一些软件的质量问题，比如会造成人死亡，你就无法明确其代价是多少。那日常工作中我们该怎么办呢，预先定好质量保证的方案和流程，广泛进行讨论后通过，然后严格按照流程去执行，不要偷工减料，最大程度的尽人事，然后听天命。**

### principle 2: quality is in the eyes of the beholder
>There is no one definition of software quality. To developers ,it might be an elegant design or elegant code. To users ,who work in stress environments,it might be response time or high capacity. For cost-sensitive projects, it might be low development cost. For some customers, it might be satisfying all their perceived and not-yet-perceived needs. The dilemma is that these may not be all compatible. Optimizing one persons quality might be detrimental to anothers.(This is Weinberg’s”Political Dilemma”principle. )A project must decide on its priorities and articulate them to all parties.

#### 质量是旁观者的眼睛
软件质量并没有明确的定义，对于开发者可能是优雅的代码和设计，对于负载压力大的用户意味着高性能的请求响应，对于高预算的项目意味着开发价格更便宜，对于有些客户意味着满足他们的提出的和未提出的需求。困难的是这些无法全部实现，满足一部分人的需求，就会牺牲其他人的需求，一个项目必须要决定它的优先事项，并且告知所有人。
#### 思考
**这一步最好在项目开始的时候就进行，把为了满足那一方的利益牺牲了什么利益都讲清楚，比如把压缩工期的可能会导致的质量问题，功能减少问题就提前告知PM，告知经理，如果能够达成一致就继续。凡事都不可能一开始都设计好，出现问题也要即使的反馈，及早的告知有影响的参与方，让他们知道自己的某项预期达不到了，早有准备。根据这本书的原则看，质量应该是最不能被牺牲的一个维度**

### principle 3: productivity and quality are inseparable
>There is a clear relationship between productivity(measured by numbers of widgits–whether they be lines of code or function points–per person month)and quality. The higher the demand for quality, the lower your productivity becomes. The lower the demand for quality, the higher your productivity becomes. The more you emphasize increased productivity, the lower your resulting quality. Bell Labs has found that, to achieve one to two bugs per thousand lines of code, productivities of 150 to 300 lines of code per person-month are common [see Fleckenstein, W,”Challenges in Software Development, ” IEEE Computer, 16, 3(March 1983), Pp 60-64].As attempts are made to drive productivity up ,the density of bugs increases.

#### 生产率和质量是不可分开的
生产率和质量是相关的，越要求提升生产率，就会导致质量下降。

#### 思考
**也说明效率的提升是有上限的，但是现实中效率的提升和改变是明显可衡量的，而质量则不是，这估计也是导致人们为了效率而牺牲质量的原因**

### principle 4: high quality software is possible
> Although our industry is saturated with examples of software systems that perform poorly, that are full of bugs, or that otherwise fail to satisfy users’ needs, there are counter examples.large-scale software systems can be built with very high quality, but for a steep price tag: on the order of $1000 per line of code. One such example is IBMS on-board flight software for NASAS space shuttle. Totaling approximately three million lines of code,the rigorous software development process resulted in less than one error found per ten thousand lines of code after product release.
>
As a developer, be aware of the techniques that have been demon-strated to increase quality considerably. These include involving the customer(Principle 8), prototyping(to verify requirements prior to full-scale development; Principles 11 through 13), keeping the design simple (Principle 67), inspections(Principle 98), and hiring the best people ( Principles 130 and 131). As a customer, demand excellence but be aware of the high costs involved

#### 开发高质量的软件是可能的
尽管现实世界的很多软件系统都质量很低，充满了bug，不能满足需求，但是构建一个高质量的大规模的软件依然是可行的，价格会急剧上升到1000美金一行代码，IBM严格的控制质量，使得一个航天飞机软件代码错误率效益每一万行代码一个bug。作为一个开发者，要知道已经被证明能提高质量的技术，涉及到客户，原型开发，保持简单的设计，检查，雇佣最优秀的额开发人员。作为消费者，要求卓越的质量，但是要考虑到花费。

#### 思考
**还是要考虑实现高质量的性价比**

### principle 5:don't try to retrofit quality
>Quality cannot be retrofit into software .This applies to any definition of quality: maintainability, reliability, adaptability, testability, safety, and so on. We have a very difficult time building quality into software during development when we try to. How can we possibly expect to achieve quality when we don’ t try? This is primarily why you must not try to convert a throwaway prototype into a product(Principle 11).

#### 不要试图改进质量
软件的质量是不能改进的，这适用于质量的定义是可维护性，稳定性，适应性，可测试性，安全性等。在尝试开发时，很难提升软件的质量。不能期望从一个原型改进成一个产品。

#### 思考
**这里的含义应该是质量的保证要在已开始设计时就体现出来，不能像做实验一样，一边实验一边开发，没有规划，没有全盘的设计，此时试图保证质量是不现实的。根据作者的理解，产品的原型应该就是验证想法，可行性的初步版本，后续完整的产品应该从头设计开发，这和目前互联网时代，快速迭代的开发应该是不太相符的，作者的时代是传统软件开发的时代**

### principle 6: poor reliability is worse than poor efficiency
>When software is not efficient, it is generally possible to isolate the sections of the program that consume most of the execution time and redesign or recode them for increased efficiency(Principle 194).Poor reliability is not only more difficult to detect, it is also more difficult to fix.A system’s poor reliability may not become apparent until years after the system is deployed–and it kills somebody.Once the poor reliability manifests itself, it is often difficult to isolate its cause.

#### 低的可靠性比低效率更糟糕
当软件的效率不高时，可以隔离这部分低效率的代码，通过重新设计，重构的方法提升其效率。对于低可靠性，不仅更难检测，而且更难修复。低可靠性可能持续数年才能被发现，而且一旦出现问题，也很难去隔离这个他。

#### 思考
**可靠性低的修复往往是牵一发而动全身，不像性能效率一样，容易发现瓶颈。正确的基础上谈效率才有意义**

### principle 7:give products to customers early
>No matter how hard you try to learn users’needs during the requirements phase, the most effective means to ascertain their real needs is to give them a product and let them play with it.If you follow a conventional interpretation of the waterfall model, the first delivery of a product to the customer occurs after 99 percent of the development resources are already expended.Thus, the majority of customer feedback on their needs occurs after the resources are expended.Contrast that with an approach, for example, of constructing a quick and dirty prototype early in the development process.Deliver this to the customer, gather feedback, and then write a requirements specification and proceed with a full-scale development.In this scenario, only 5 to 20 percent of the development resources are expended by the time customers experience their first product.f the appropriate features were built into the prototype, the highest-risk user needs will become better known and the final product is more likely to be user-satisfactory.This helps ensure that the remainder of the resources are spent building the right system.

#### 尽早的交付产品给客户
无论前期需求分析阶段多么努力的了解客户的需求，都不如给客户一个产品，然后他使用产品，从中发现需求。如果遵循瀑布模型开发，第一次交付给用户时，开发资源的99%已经被耗尽了，此时才能从客户身上得到反馈。于此相反，在开发早起构建一个不完善的原型，然后给客户使用，获取反馈，然后再写需求分析，进行全量的开发。此时第一次交付时只消耗了5%到20%的资源。通过原型验证，发现客户真正需要的功能，这样保证了开发资源都被用在了正确的事情上。

#### 思考
**对于互联网产品尤其适用，先用小的代价实现一个效果可能没那么好的版本，然后看消费者的使用情况，然后进一步改进。不过这里有一个问题就是，有可能这个比较差的原型上线后，尝鲜型的使用者用后，由于效果不好就放弃了，即使我们后期改进了一个更好的版本，可能这部分人也不会再使用了，失去了对产品的信任。这样，是不是就需要功能效果完善后再上线了呢？这其中的度是最难把我的**

### principle 8:communicate with customers/users
>Never lose sight of why software is being developed:to satisfy real needs,to solve real problems.The only way to solve real needs is to communicate with those who have the needs.The customer or user is the most important person involved with your project.If you are a commercial developer, talk often with the clients.Keep them involved.Sure, it is easier to develop software in a vacuum, but will the customer like the result?If you’re a producer of shrinkwrap software,”customers”are harder to locate during development.So role-play.Designate three or four individuals in your organization as prospective customers and tap them for ideas that will keep them as customers or make them happy.If you’re a government contractor, talk often with the contracting officers, their technical representatives, and, if possible, the users.People and situations change often in the government.the only way to keep up with the change is communication.Ignoring the changes may make life seem easier in the short term, but the final system will not be useful.

#### 和用户交流
永远不要忽视为何进行软件开发，是为满足现实的需求，解决现实的问题。必须要和有问题的人交流才行，用户是项目中最重要的参与者。沟通的目的是为了了解变化，如果忽视变化，短期内生活会变容易，但是长期来看就没效了。如果开发时客户比较难以确定，可以在项目内部指定几个人扮演客户的身份。

#### 思考
**互联网项目中，toC产品中还能找一些人调研，使用，但是对于toB产品来说，用户就是一个企业了，就不那么具象了，如何提升其在项目中的参与程度？应该还是要落实到具体企业软件使用的人身上，还有企业的问题和发展诉求。而且目前很多公司都是产品经理，运营人员接触客户较多，作为开发人员反而没怎么直接接触用户，客户的想法通过产品经理传到开发人员那里，可能会有偏差，由于身处项目中的角色不同，开发人员和产品经理看待问题的角度也会不同。**

### principle 9: align incentives for developer and customer
>Projects often fail because customers and developers have different(and perhaps incompatible) goals.For example, take the simple case in which the customer wants features 1, 2, and 3 by a specific date and the developer wants to maximize revenue or profit.To maximize revenue the develper may attempt to build all three features in their entirety even if late.To maximize revenue the develper may attempt to build all three features in their entirety even if late.To help align the two organizations’ goals:
(1)Prioritize requirements (Principle 50)so that developers understand their relative importance,
(2) reward the developer based on the relative priorities(for example, all highpriority requirements must be satisfied, each medium priority requirement earns the developer a small additional bonus of some kind and each low priority requirement satisfied earns a very small bonus),
(3)use strict penalties for late delivery

#### 调整开发者和客户的奖励机制
项目会由于客户和开发者的目标不一致而失败，比如客户需要1，2，3个功能在特定的日期，而开发者为了最大的利益会统一开发这个3个功能，即使会延误交付日期。而客户也只能先失去某些功能，直到其他的功能开发完毕。为了对齐两者的目标，1.把需求分优先级，让开发者明白什么是相对重要的；2.就相对的优先级来给开发人员付报酬，比如所有的高优需求必须满足，每个中优需求会给开发人员带来额外的奖励，低优需求带来小的额外奖励；3.对于延期指定严格的惩罚措施

#### 思考
**开发者应该把上述为了提高收益而合并开发的事情提前告知客户，争取达成一致，作为条件可以附赠一些低优的功能。开发人员也要有好的设计能力，使得程序有可扩展性，能够适应未来可能有的变化，尤其是后续的变化是目前低优，中优的需求，那么大概率未来可能还是要开发，所以要提前设计好。**

### principle 10:plan to throw one away
>One of the most important critical success factors for a project is whether it is entirely new.Programs that tread on brand new territory(whether it be with respect to application, architecture, interface, or algorithm) rarely work the first time.Fred Brooks, in his Mythical Man Month, makes this perfectly clear with his advice, “Plan to throw one away; you will anyway.”This advice was originally presented by Winston Royce in 1970, when he said one should plan for the first fully deployed system to be the second one created.The first should at least check out the critical design issues and the operational concept.Furthermore Royce recommended that such a prerelease version should be developed with approximately 25 percent of the total system development resources.As a developer of a new custom product, plan to build a series of throwaway prototypes(Principles 11, 12, and 13)before embarking on the full-scale product development.As a commercial high-volume developer expect that your first product version will be able to be modified for a certain period of years, after which it will need to be fully replaced(related Principles 185, 186, 188, and 201).As a maintainer of a product, be aware that you can fiddle with the program just so much before it becomes unstable and must be replaced (see related Principles 186, 191, 195, and 197).

#### 计划扔掉一个
项目成功的最重要的一个原因就是这个项目是否是新的。进入全新领域的程序很少能第一次就工作正确。有一句话说到，计划丢掉一个，你迟早还是会拥有的。第一个完全部署的系统应该是由前一个升级来的。第一个版本应该能够检查出设计的问题，以及操作理念的问题。进一步，这个第一个版本应该用25%的总资源来开发。作为一个新的项目的开发人员，应该做好准备丢掉一系列构建的原型。作为一个大的商业软件的开发人员，要保证你的第一个版本能够后面数年被持续修改。作为一个项目的维护人员，在程序变得不稳定，必须被替换之前，你可以对程序做持续的修改。

#### 思考
**这里应该要表达的就是原型开发，和程序要有可扩展性，可以持续进化改进。而且第一个原型往往是用来验证的，后续可以扔掉他，在其基础上再做新的。问题在于，一个项目持续几年后，由于人员的变动，代码文档的不健全，导致后面的升级和修改越来越难做，后面的开发人员也不敢对项目进行升级改进了。那么此时该怎么办？如何衡量什么时候该重新做一个新项目替代他，还是继续保持现状，这里当然要衡量两者的代价，可是低价的标准不太好定，基于质量是第一位的，我觉得应该当老的项目由于维护性差出了线上严重问题时，就要考虑替换了，单纯的考虑人力成本，那开发新项目的成本无论何时基本上都会大于修改老项目**

### principle 11:build the right kind of prototype

#### 构建正确的原型
有两种原型，需要抛弃的原型和可以进化的原型。可抛弃的原型是快速构架，用来获取客户的反馈，明确需求的。可进化的原型是在严格的质量保证下开发的，给客户用来获取反馈，然后根据需要进行修改，反复迭代直到产品完全满足需求。可抛弃原型的用途是当重点的功能不能被清晰理解，明确时。可进化的原型是重点功能明确，但是其他功能不清晰时。如果大部分功能都不明确那么就需要以进化原型的角度构建一个可抛弃的原型

#### 思考
**现代这中可抛弃的原型估计就是设计图或者纯前端就可以搞定了，对于可进化的，即需要持续改进的，就需要保证设计是兼容性强，可以灵活变动的，不然后续的每次修改代价会越来越大，操作中可以每完成几轮迭代后就抽出部分时间，进行代码的重构，保证结构的优雅，便于进一步开发，如果是长期项目，考虑到人员的变动，文档等也要更加完善，以让后面的人可以接手**

### principle 12:build the right features into a prototype

#### 在原型中构建正确的功能
当构建一个可抛弃的原型时，应该只开发哪些不清晰的功能。开发哪些明确理解了的功能，不能学到任何东西，并且浪费资源。构建进化原型时则开发哪些被最明确的功能，期望用户通过使用这些功能，让用户决策是否需要附加额外的功能。如果在进化原型中开发了不明确的功能，那么就有可能需要抛弃这个“高质量”原型的风险，浪费资源

#### 思考
**商业软件，外包开发时能够明确客户的需求，对于互联网产品，客户有时候是潜在的，并不直到自己的需求，这个需求往往是开发团队自己确定的，开发了原型然后到市场上去实验，此时抛弃这个原型与否的就是市场了**

### principle 13:build throwaway prototypes quickly
#### 快速开发可抛弃的原型
开发可抛弃的原型要尽可能的快，不要担心质量，用一个页面满足需求，不要担心设计和代码质量，使用任何可以利用的工具，任何语言，不要在乎语言的特性

#### 思考
**有时候是不是都可以不用编程实现？**

### principle 14:grow systems incrementally
#### 增量式的开发系统
一个有效的减少软件开发风险的方法时逐步递增的开发软件，从一个只实现了几个小功能的系统开始，然后逐步扩大涵盖越来越多的功能。优势是1.每次构建风险低；2.看到一个版本的产品后，容易帮助客户发现他们还需要什么功能；劣势是如果已开始选择了不合适的架构，那么后续就需要重新设计，以实现新的功能。通过开发抛弃型的原型来避免这个风险。

#### 思考
**脚手架的作用，最小的起步集合。对架构设计的要求比较高。现在的做法似乎是微服务，把大的系统拆成小的服务，每一个自己互相独立，单独部署，互不影响。这样先开发核心的服务，然后再开发非核心的，由于进行了一次拆分，每一个服务的功能复杂度下降，也降低了设计的复杂性**

### principle 15:the more seen, the more need

#### 看到越多需要的就越多
已经被证明，给用户提供越多的功能/性能，用户就会需要更多的功能/性能。你必须要对此做好准备，无论是经理还是工程师，一旦客户看到了一个产品，他们就会需要更多。这也意味着，每个开发文档都行开被保存和管理好，以备将来。意味着配置管理也应该在发布很久前就完善，要准备好应付客户的口头和书面的请求，也意味着设计要选择的够好，足够支持功能的变化，和性能的提升需要。

#### 思考
**对于互联网产品，用户不是一个特定的人，每个人需要的不一样，他们看到第一个版本的产品后，也会有很多新的想要的功能，我们必然不能全部接受，要有权衡的去实现。虽说设计时要考虑到性能，和功能的后续变动，但是亦不可过度设计。这其中的折衷点在于，如果后续的变化能带来的收益足够支持重新开发新的系统，那么一开始的系统能满足达到这个收益前的需求即可**

### principle 16:change during development is inevitable
#### 开发过程中的变化是不可避免的
无论你在软件开发的那个阶段，系统的变化都是不可避免的，这种变化会持续整个阶段。软件系统的变化和软件不是后导致需求的变化并不一样。这种变化体现在新的代码，新的计划，新的测试，还有修复产品中新发现的错误，或者提升现有产品的性能。为了让自己能够准备应付这些变化，要保证软件开发中的各个产品是交叉引用的？每次更新的管理要到位。预算和开发的排期要留上buffer，以防哪些关键的更新没有资源开发

#### 思考
**需要花费的时间总比我们预计的要多**

### principle 17:if possible, buy instead of build
#### 如果有可能，购买而不是自己构建
唯一一个最有效减少软件开发花费日益扩大的方法就是买一个软件，而非从最原始的开始开发。购买的软件只能满足75%的需求，但是可能要花十倍的价钱才能开发一个100%满足需求的软件，而且还要承担超过预算，逾期的风险。而等它开发完后可能会发现，其依旧只满足了75%的需求。作为一个消费者，新的软件开发项目一开始看起来总是令人兴奋的，团队会乐观于完美的方案。只有很少软件开发的过程是顺利的，逐步升高的预算会导致部分功能会砍掉，最后和在售的软件系统提供的功能差不多。作为一个开发者，你需要尽可能的重用软件，重用就是购买而不是自己构建。

#### 思考
**大多数时候自己开发的成本可能更高，比如检索系统自己开发而不用ES，虽然我们会找一堆理由，一堆新功能，但是最后花了很大的代价，而且公司内部往往KPI考虑，从零开始开发的KPI收益会大于复用之前的。另一方面，现成的软件，尤其是开源的，可能通用性很高，但是对于公司自己的业务，可能并不完全match，导致部分的性能浪费，部分功能无法实现。如果，性能是项目的关键，这个缺失的主要功能是项目的关键，那么我认为还是有必要开发新的系统**

### principle 18:build software so that it needs a short users's Manual
#### 开发的软件要有一个尽量短小的用户手册
一个衡量软件质量的方法就是查看其用户手册的大小。手册越短，软件质量越好。一个好的设计的软件应该是自说明的。不幸的是，太多的软件设计者把自己说成了一个人机交互界面设计的专家，但是大量的手册证明，他们并不如他们声称的那么优秀。使用标准的接口/接口。使用工业级的专家去设计自说明的图标，命令，协议和用户界面。并且记住，只是因为软件开发者喜欢这个接口/界面，并不意味着你的客户会知道如何使用它。许多软件开发者用一些tricks的技术构建了简短，省略的接口。通常，客户喜欢的是简单，清晰的接口，并不是trick的。

#### 思考
**这一点，作为普通的2C产品，或许大多数开发人员还能考虑的周到，但是作为2B的软件，或者作为公司内部的软件，往往设计的就每那么好。商业软件，里面功能众多，及其复杂，作为开发人员可能尚不了解全部功能的使用，更不要提普通小客户了。但是由于商业系统可能以帮助客户赚钱/省钱为目的，这方面的容忍度一般B端软件比C端软件的客户要大。另一方面，公司内部开发的系统和平台，开发者往往觉得自己会用，就认为别人也会用，即使大家都是开发人员，但是不具备你的背景，那么也不一定了解你的产品怎么用，从而导致后续有复杂的，疏于维护的wiki，增加了许多使用上的沟通问题，并且导致了反复造轮子，反复开发原有功能。**

### principle 19: every complex problem has a Solution
#### 每一个复杂的问题都会有一个解决方案
有人说，“每一个复杂的问题都会有一个 **简单的*#### 解决方案，这是错的”，要高度怀疑，如果任何人告诉你，“跟随以下10个简单的步骤，你的软件质量问题就会解决”
#### 思考
**复杂问题会有一个解决方案，但是这个方案可能不一定简单。同时自己有一个经验，可以补充一下，80%复杂的问题（尤其指bug），其实都是由一些简单的小问题造成的，比如少些一个字母，大小写错误，编码错误，误删除了一行代码等等。因为这种错误不在我们的预期之内，所以程序后续的错误会让我们觉得很复杂，无从下手，不必太过慌张，仔细检查，能解决大多数的问题。**

### principle 20:record your assumption
#### 记录下你的假设
我们部署软件的软件可能是各种各样的，并且不可能全部明晰。当我们构建软件，在这样的一个环境中去解决问题时，我们就会对这个环境有许多假设。有人说每10行，每20-30行代码就会有一个假设。有限的假设和无限可能的真是世界，就会产生问题。比如有些假设，最后就会被验证是错误的。需求分析，设计，编码，测试时，不可能会注意所有的假设。所以，建议用一个本子记录下所有的假设。即使这些假设看起来显而易见，或者如果不这么假设是显然违反常理的。同时也要记录下假设的实现，这样就能和项目中的该假设对比，看其是否体现了出来。理想情况下，每一个假设都会有一个实现进行封装隔离。

#### 思考
**有假设就要考虑假设的可行性，不能太理想化，有一些错误必须要考虑。假设要尽可能的正确，所有有些关键的假设要找数据，方法去论证其正确性。比如一个流量预估系统，我们会有一个假设，每天的流量是差不多的，每个词上的流量也是差不多的，这样才能预估。但是这个假设本身对不对呢？作者把假设进行封装的思想很有意思，减少假设之间的耦合性，这样一旦现实环境的某一项变化了，针对其的假设就可以轻易的变化。**

### principle 21:different languages for different phases
#### 不同的阶段用不同的语言
工业界的终极渴望是用简短的方案解决复杂的问题，这驱动了许多声称最好的软件开发方法，可以用同一套符号来描述软件开发的整个生命阶段。既然这种方案不存在于其他的工程科学中，那为什么会存在在软件工程中呢？电器工程师用不同的符号语言，在不同的设计活动中。符号提供给了我们模型去描述我们脑中的思想，越多的符号就会越丰富我们表达的方式，从而我们就能更好的理解，具体化我们的产品。为什么软件工程师在需求分析，设计，编码阶段用同样的语言？为什么要把面向对象用在程序开发的所有阶段呢？在不同的阶段之间转化是很困难的，用相同的语言也无济于事。当然，如果一个语音真的那么理想适合多个阶段，那就果断用它。

#### 思考
**不能迷信面向对象编程，和函数式，过程时都要用，那个合适用哪个，现在语言中的lambda表达式就是函数式编程的东西。如果一个方法和类中的对象并没有什么关系，那么完全可以独立出一个函数，对于明显过程化的业务， 比如报表之类的，就很时候面向过程开发**

### principle 22:Technique before tools
#### 技术在工具之前
一个没用经过训练的木匠，给他厉害的工具，他会编程一个危险的新手木匠。一个没经过训练的软件工程师也是同样。当你使用一个工具时，你需要被充分训练过，了解工具，并且遵守软件开发的技术。当然也需要知道如何使用工具，当然这相对于好的训练来说是第二位的。强烈建议手工的的实现一个技术，并且向你自己和经理证明这个技术是可以工作的，在引入自动化的工具之前。大多数情况下，如果一个技术在非自动化时无法工作，那么自动化了也不能用。

#### 思考
**使用一个工具时要了解其原理，知其然也要知其所以然，比如用valgrind去分析C++程序，要了解其原理，知道这个原理是可行的才可以开发这样的工具。先用原始的方法验证技术，然后再自动化，自动化是为了效率的提升，但使用技术解决问题才是真正的价值。**

### principle 23:use tools, but be realistic
#### 使用工具，但是要注意现实
软件工具会帮助它的使用者提升效率，无论如何请使用他们。就像一个文字编辑器是作家有效的帮手，一个CASE工具对于软件开发者也是大的助力。提升初始化工作10-20%效率，提升修改效率25-50%。但是软件开发最重要的工作，思考，是无法通过工具完成的。要真实的评价CASE工具的使用对生产力的提升，大约70%的CASE工具被购买后没有使用。我觉得首要原因是对工具过分乐观了，然后结果是令人失望的，而非工具本身没有效果。
>CASE tools 为Computer-Aided Software Engineering tools的缩写，意义为“计算机辅助软件工程工具"。 目标是通过一组工具和方法使软件系统成为一种高质量，规范化，方便维护的软件产品。 它也涉及到信息系统发展中所使用的方法和自动化领域中软件开发相关内容。

#### 思考
**软件开发的10%的工作才是编码，对于个人来说思考花的时间多，对于整个团队来说用在沟通协作上的时间更多。工具并不能大幅度的提升效率，尤其是对思考而言，从而也不要迷信有什么工具的引入会大幅缩短开发时间。对于沟通来说，好的软件倒是的确能提高效率，但考虑到沟通的本身也是思考的一种体现，所以其能做到的也是有限**

### principle 24:give software tools to good engineers
#### 给好的工程师工具
文字编辑器能提升作家的效率，但是不能把一个糟糕的小说变好，工具也不能把一个糟糕的软件工程师变成优秀的。只给好的工程师工具，因为给了差的工程师工具，反而会提升他们生产低质量代码的效率。

#### 思考
**质量本身无法通过工具提升，不过工具现在倒是可以提供检测，告诉你代码的质量，从而让你修改，从这一方面看，这种工具相当于提升了工程师的基础素质，也激励了优秀者想要优秀，需要更加的努力。**

### principle 25:CASE tools are expensive
#### CASE工具的价格是昂贵的
主要考过购买价格，软件使用的培训费用，后期每年的许可费用，CASE是有用的，也是要做必要的投资的，要分析预算和回报时考虑到CASE工具的高额花费，但也要考虑到，不买这个工具可能会带来的更好的费用，比如低的生产率，质量，延期交付等成本。

#### 思考
**一个工具的是否使用，一件东西的买与不买，不能只看价格的贵与便宜，要看投入产出比，哪一种性价比更高就选择那一个，不要拘泥于定式。我们会觉得日常看法中，软件工程的项目管理相关软件的使用非常麻烦，各种卡片，流程要走，看似是一个不小的代价。但如果没有这些可能导致的代价会更大。这个地方的难点就在于，不是所有的东西都那么容易衡量价值，代价。**

### principle 26:know-when is as important as know-How
#### 知道何时做和知道如何做同样重要
在软件开发中，经常有一个工程师学到了一项新技术，并把它当作解决其他一切技术的替代。于此同时组里另一个工程师也是如此，于是不可避免的成轮就发生了。事实上两者都不对。知道如何使用一个新技术，不能使这个技术变成一个好的技术，同时也不能使你自己成为一个优秀的工程师。就像会使用木工车床不能让你成为一个优秀的木匠。优秀的工程师知道数十种不同的技术，并且知道在一个项目中何时该使用其中那一个。当做需求分析时，要知道那种技术最适合解决当前的问题。做设计时要只能那种技术最能描述系统，做编码时选择最合适的编程语言。

#### 思考
**对于初学者来说，不必纠结于该学JAVA还是C++，这俩你都需要会，还需要会Python，Go，Shell等等。同时也要明白一个新技术出现的背景，和他适用的问题，不要人云亦云，看Go出来了，就什么项目就像用Go。不要会了多线程技术，就什么都要多线程，同时，线程池，缓存，生产者消费者模型，protobuf等都是这样。比如最近我的一个项目，为了提升效率，直接把二进制进行持久化，而不用protobuf。**

### principle 27:stop when you achieve your goal
#### 达到目标时就请停止
软件工程师会用多种方法和技术，它们每一个都是为了一个目的出现的，同时又是为了解决项目中的一个子问题。比如面向对象分析的目标是了解要解决的问题。比如DARTS的目标是架构设计等。每一个情况下，这个技术会包含一系列的步骤，不要为了应用这个技术而忘了问题本身。不要对目标的变化有负罪感。如果你发现这个技术应用了一半，问题就解决了，那么及时停止。另一方面，也要有软件开发的全局视野，要明白这个技术后续的步骤的增加，可能会导致其他的风险，从而产生新的问题。

#### 目标
**这点感觉在互联网的开发中，大家重视效率，一般都是开发到能用就上线了，有时候可能有些必要的步骤都还没做，这种做了过多的步骤的情况似乎并不多见。可以从其他方面理解，比如不要为了炫技，目标是解决问题。不要过度设计，过度考虑容错，从而引入了过多复杂的保障性措施，从而使得问题的解决占的比例下降**

### principle 28:know formal methods
#### 要知道形式化方法
形式化方法如果没有很强的离散数学功底是很难掌握的。从另一个方面说，使用形式化的方法能明确软件开发中许多没有覆盖的问题。每个项目中至少要有一个人能够熟悉形式化方法，从而保证构建的软件是有质量的。许多人认为唯一需要使用形式化方法的地方是用他们来详细说明一个系统的完成度。这个理解并不对，事实上，最高效的方法是写一个口语的说明书。然后试着用形式化的方法写其中的部分。试着用形式化的方法来书写会帮助你发现口语中的问题。进一步修改口语中的问题，就能等到一个好的说明书。在形式化主义帮助你后就请忘了它。

#### 思考
**形式化有严格的规则，能帮助明确问题，提高系统的可靠性和健壮性，成本高**

### principle 29:align reputation with organization
#### 把名声和组织结合在一起
日本软件工程师看待软件bug的佳都不同于美国工程师。其中一个差异是，在日本一个产品的错误会让公司丢脸，公司的丢脸又会导致软件工程师愧作为一个工程师。这产生的原因是相对于美国，日本工人一般会在一家企业工作一辈子。通常，当任何人发现一个软件中的错误时，工程师应该是感恩的，而不是又挫败感。会产生错误才是人类。接受它，克服它。发现错误应该把它告诉其他人，而不是隐藏它。把错误告诉其他人可以避免其他人犯同样的错误。也可以为了未来没防范的错误被修复做好准备。

#### 思考
**和公司的KPI设定有关，一个错误的发生不能让一个人完全背锅。应该合力去解决。Case Study也是必要的，不是为了批斗，检讨而是为了从中学习，这个问题涉及到人性，很难处理，一定要从文化上去引导。如果一切符合规则，流程，犯了错误就不能只指责某个人。Case study时，其他的人也应该说下，如果自己遇到这样的问题该怎么办，而不是只有犯错的人反思。**

### principle 30:follow the lemming with care
#### 小心从众
5000千万人认同一件愚蠢的事情，它依旧是愚蠢的。比如面向对象，软件管理，软件重用，CASE工具，原型开发。这些东西都是这样，适用的公司用了才会又效果，要考虑自身的情况。当学习一个新技术时，不要很快的就全盘接受。仔细了解，小心其中的风险和代价。做必要的试验。

#### 思考
**乌合之众。不要盲目的随大流，要有自己的思考，如果自己思考后认为的确是这样，那么跟随大众就没问题。也不是为了特立独行而特立独行，关键是要有思考。对于软件开发，还是要了解每个技术，方法的存在背景，适用场景，以及它的trade off。**

### principle 31:don't ignore technoloy
#### 不要忽略技术
软件开发技术日新月异，你不可能长期保持不变，如果缺少对新技术的学习。技术的发展往往是一个一个的浪潮，通常一个浪潮5-7年，新的浪潮在之前最高效的技术上面又进一步的发展。两个保持自己对新技术的渴求的方法就是，1读正确的杂志，2和正确的人交谈。不要只和自己公司的人交谈，每年参加一两次会议。会议中的演讲可能不如你在大厅里与人的交谈。

#### 思考
**持续学习，不要不了解一个东西就去嘲笑它，比如最近的区块链，有些人看不起这个技术，认为都是骗钱的，应该先去充分了解学习。不能只依靠网络上的博客文章的知识，要寻找可以交流的人，思想要进行碰撞，交流才能互相精进。以后参加会议，要多搭讪认识不同的人，不能只傻傻听**

### principle 32:use documenttation standards
#### 使用文档化的标准
组织和项目中又标准就要遵守，永远不要把做了一件错误的事情，怪罪到标准上。遵循标准的基础上也要革新，要有智慧的遵守，即使你没有被要求遵守某项准则，也可以拿一个准则作为checklist。

#### 思考
**要灵活的变通，不能过于死板。比如代码规范，也有可以豁免的情况。上线的功能，如果没有影响可以先带上去等等。原则性的规范不要违反，其他的灵活调整。作为管理者也要了解这点，不能苛求员工。**

### principle 33:every document needs a glossary
#### 文档都要有一个词汇表
文档中要有一个词汇表，以免读到不明白其含义的词的时候有地方可以查。一个做法是，在一个专业名词出现时在下方有常见的话进行解释，然后再用专业的定义进行解释。

#### 思考
**体现出一个思想，你写的文档，代码，等是给别人看到的，要站在别人的角度上思考问题，别人可能是初学者，也可能是专业人士。**

### principle 34:every software document needs an index
#### 每个软件的文档都需要一个索引
文档中有一个列表，标注了每个词和概念出现的位置和页码。在需求分析，设计，编码，测试，用户手册中的文档都需要。尤其是在后期软件的维护和升级中。现在的文字编辑器有这些自动化的功能来生成索引。

#### 思考
**反观公司的商业化的软件，使用复杂不说，配套的用户文档也十分不健全，使用困难。现在很多地方采用了视频化的文档，但是这种效率较低。其他阶段的文档就更不健全了，而且关键的是更新不及时。很大的原因时，互联网的软件开发生命周期都太短了，一个产品一共也就一辆年，不像传统软件一开发就是一两年。**

### principle 35:use the same name for the same concept
#### 相同的概念用相同的名字
和小说不一样，技术文档要用相同的词表达相同的概念，相同的句式表达相似的信息。

#### 思考
**日常的开发中，有时候同一个项目都有不同的名词，有时候用项目代号，有时候产品名称，有时候又用简称。增加交流成本。写技术文档时，要明确不要各种修饰，词藻。**

### principle 36:research-then-transfer donesn't work
#### 研究然后转化为现实的道路并不好用
有不少软件工程技术被研究出来，但是很少使用。1.通常软件研究者的实际开发部署经验少。2.研究人员发现的某种简单技术解决问题的方法，并没有经过大量时间的验证，这个方法是否真的适合现实环境。3.研究人员和实际开发人员有很多分歧，互相难以交流。把研究结果转化为工业中切实可用的方案，一个方法就是增强两者之间的联系，用真实的环境。

#### 思考
**这可能是这个上个时代容易出的问题，现在学校科研机构和工业界的结合比以前要好多了。不过也提示我们切记闭门造成，要及早的到现实世界中去验证**

### principle 37:take responsiblilty
#### 负责任
在所有的工程原则中，当一个设计失败，工程师会被责备。比如在桥梁坍塌后，我们会问工程师做错了什么。但是当软件失败时，却很少责备工程师。软件工程师有很多借口逃避责任，所以就会导致糟糕的设计。There are no excuses。如果你是系统的开发容易，你的责任是保证系统正确。负责任，要么就不要做。

#### 思考
**责任心，的第一步是完成交代的工作，对齐质量，结果负责。第二步就是要有Owner精神，对整个项目负责。原则性的错误不能去反，无法避免的错误要用丰富的知识和经验，尽量去避免。**

## chapter 3:Requirement engineering principles 需求分析准则
需求阶段两个过程，1，学习这个需要一个解决方案的问题。2.封装一个黑盒系统来解决问题

### principle 38:poor requirement yield poor cost estimates
#### 差的需求分析，导致差的预算估计
利用原型开发减少不正确的需求的风险，利用配置管理来控制变化。计划好未来发布后会有新的需求。用更加正规的方法去做需求分析。

#### 思考
**会有项目开发一半了，发现要推到重来。PM和RD要沟通好，RD要明确PM的需求，可以通过复述的方式。同时PM也要真的理解客户的需求，这一步可能更难一些，不能过分依赖调研，调研的结果有时候有导向性，有时候客户会潜意识的欺骗。**

### principle 39:determine the problem before wrting requirements
#### 在写需求之前先要决定问题是什么
不能一面对问题，就不去思考，立马开始提供方案，要进行分析。一个大楼里，租户觉得等电梯的时间长了浪费时间，作为大楼里的管理者，觉得是租户多了，而不是电梯少了。于是方案应该是增加电梯的速度，而不是增加新电梯，提高租金，甚至修改电梯算法等方法。遇到问题时要尽可能的考虑都有谁，遇到了什么问题。当解决问题时，不要被第一个令人激动的方案所迷惑。流程上的一些改变会比构建一个系统便宜的多。

#### 思考
**一个问题中会有参与的多方，要从不同方的角度思考问题。就像广告系统，不能只考虑到商家，也要考虑到消费者，这样就会明白，消费者不愿意看到不感兴趣的恶趣味广告，于此同时消费者也确有购买商品或者服务的需求。**

### principle 40:determine the requirements now
#### 现在就决定需求
需求是很难理解和明确的。一个错误的做法就是潦草的明确需求说明文档，然后就冲过去开始设计和编码。这种错误的方法的假设是：1.任何系统都好过没有系统。2.需求迟早会明确。3.设计人员会在构建系统的时候指出什么能够构建开发。正确的方法是，当前要尽可能的了解和学习需求。做原型，和客户交谈，收集数据。然后再文档化需求。逐步迭代增量的开发，但是每次增量的开发都不能没有好的需求分析。

#### 思考
**人们总是相信行动比不行动好，有时候并不这样，要观察和思考。这里要有作者提到的一些分析的方法，也不能干想而不动手，长期没有可见的进展容易导致人心涣散，缺乏干劲，要把明确需求深入到骨髓中去。**

### principle 41:fix requirements specification errors NOW
#### 现在就修复需求说明中的错误
需求说明中的错误，会导致后期的工作用几十，上百倍的代价修复它。

#### 思考
**一定要尽早的发现问题，如果是不确定的问题，觉得有风险的要及时抛出，给合作同学，上下游知道。**

### principle 42:prototypes reduce risk in selecting user interfaces
#### 原型可以减少选择用户界面的风险
开发界面非常简单，不但能明确需求，好的界面也会赢得客户的信心。

#### 思考
**互联网中一般不好直接给用户提供只有一个界面的原型，多少还是要有一些功能。不过设计人员开发早期的界面原因，能让整个团队对产品有更直观的感觉，便于明确问题。一图胜千言。这也是为何UE重要，现在PM一般要有这种界面设计的能力，便于提需求。**

### principle 43:record why requirements where included
#### 记录下在何地，为何引入了这个需求
记录下需求引入的时间和背景，这样后续有变更的时候可以溯源

#### 思考
**现在大多交流以IM工具进行，加上邮件，天然有记录，但是为了管理方便，对于会议要有会议总结，需求的修改要及时更新到MRD文档中，并让相关同学及时知晓。**

### principle 44:Identity subsets
#### 定义子问题
定义需求的最小集合。每次增量开发的最小集。记录下每个版本包含的功能集合。甚至要记录不同的客户，不同的版本有哪些功能。

#### 思考
**就是功能分优先级的思想，对于2B的商业软件，会有不同客户的不同定制化功能，也要进行分类和管理。对于开发人员来说，要写明白每个代码CI的注释，便于分辨哪些关键功能是哪些版本加入的。**

### principle 45:review the requirements
#### 检查需求
自然语言写的需求不利于后续的检查，应该用更规范正式的语言来写需求。

#### 思考
**把聊天确定的需求文字化，把文字化的东西正规化。**

### principle 46:avoid design in requirements
#### 避免在需求分许时提前开始系统设计
需求阶段的目的是指出系统额外的行为。额外的行为需要非常明确，以让不同的设计师都能达到一致。需求的时候不能明确软件的架构或者算法，这是设计人员要负责的事情。如果写需求的人发现很难明确额外的行为，除非用一些看起来是设计的东西，比如状态机等。需求人员应该给设计人员提示

#### 思考
**自己经常一边分析需求，一边就陷入设计中。应该把这两件事分开，讨论需求时先不要想要怎么做，甚至都不用考虑能不能做。先明确想做什么，做出来的东西能有什么功能。然后再看下一步。只不过一个人负责这两部分时，往往分的没那么开。**

### principle 47:use the right techniques
#### 使用正确的技术
没有万能的技术适合任何应用的需求分析，复杂系统的需求分析要用多种技术。比如，使用entity-relation diagrams设计数据密集型的应用。有限状态机分析交互式实时系统。Petri nets针对同步性的挑战，决策表用来分析决策密集型的应用。

#### 思考
**平时自己的确很少用到上述方法来分析，一般都是文字描述需求，对于复杂的系统还是要借助一些形式化的手段，使得信息的表达更清晰**

### principle 48:use multiple views of requirements
#### 利用需求的多面视角
从任何一面看需求，都是不够的，不能完全理解这个复杂系统的一些额外的行为的。要综合利用结构分析，面向对象分析，状态表分析等手段。比如面向对象，对真实世界进行分析，让你明白对象之间的关系和相关属性。利用有限状态机来表述用户接口的行为。用决策树来描述系统响应复杂的条件组合的请求时的结果。

#### 思考
**需要在实践中加深印象，不过互联网公司追求快速，对需求分析的文档要求的就更不严格了。要结合实际，精炼的表达需求，也不要太拘泥形式**

### principle 49:organize requirements sensibly
#### 合理的组织需求
我们通常会水平的组织需求。组织需求要便于别人阅读需求，便于修改人定位需求，进行修改。要依据不同的产品采用不同的组织方法。可以按照应用中的参与方，来组织，比如用户，商家。也可以按照大的功能来拆分描述。

#### 思考
**公司中的项目往往一个个的都很小，组织形式都是按照Web页面上的功能划分来写的**

### principle 50:prioritize requirements
#### 区分需求的优先级
并不是所有的需求都一样重要。一个方法是给每个需求加上前缀。M mandatory，D desirable， O optional。更好的方法是分0-10级。

#### 思考
**工作中应用的尤其多，主要就就是解决资源和需求的不匹配。一般能分成两个优先级就可以了。**

### principle 51:write concisely
#### 需求要写的简明

#### 思考
**结合前面的一条，不要加上各种修辞要用相同的话术表达相同的概念。**

### principle 52:separately number every requirement
#### 给每个需求编号
每个需求都要能被简单的索引，这有助于后续的设计和测试阶段。简单的做法就是每个需求加一个独一无二的TAG，或者每个段落，句子用字母编号。然后可以自动化的解析这些标记

#### 思考
**后续测试时的case list，就是要对应上前面的每个需求，这样就便于把case list和需求关联起来，明白有什么功能没测试到。所以能不能用excel来写需求文档？**

### principle 53:reduce ambiguity in requirements
#### 减少需求中的歧义
大多数需求用自然语言来书写，而长用的词，或句子很容易有歧义。只有使用正规的语言才能消除歧义，平时也可以通过重写有歧义的段落来消除歧义。有以下三个方法消除歧义：1.利用fagan-type检查SRS。2.利用正式的模型来重写需求中的问题。3.重新组织SRS，使得自然语言和正规模型写的部分分开。

#### 思考
**工作中没有这么复杂的需求文档，一般都是开发人员再次复述确认下需求。或者可以让客户再次复述下需求文档的意思，看是不是书写文档人的本意。这里的问题就在于，一般只有认为有问题的才会确认，有的你可能认为自己理解的就是对的，于是就不会再确认。所以需求文档的描述还是尽量要规范，这样也减少沟通的成本。**

### principle 54:augment, never replace, natural language
#### 增加而不是替代原来的需求描述
在减少需求文档中的歧义时，一般会利用概念，定义来替代自然语言，比如利用状态机，预判逻辑，状态表等。但是这样整个需求文档就会让其他人不太容易理解，比如哪些有很少计算机科学知识，数学背景的人。解决的方法就是同时保留原来自然语言描述的需求。可以用一页的正反两面来分别描述。这样其他人也能读的懂

#### 思考
**文档一方面是让专业的人读，有的时候也会有非专业的人读，尤其是面对普通客户时，要让两者都能看得懂，明白你的需求，这样才能知道写的对不对。**

### principle 55:write natural language before a more formal model
#### 在采用格式化的模型描述需求前，先用自然语言写
如果先用正规的模型去描述了需求，那么后续的自然语言描述就会倾向于去描述这个模型，而不是描述解决问题的系统了。本末倒置。最好的方法是，1.先用自然语言描述2，再用模型描述，3，再调整自然语言的描述以减少歧义。

#### 思考
**需求文档要描述系统的功能，切记为了形式化本末倒置。**

### principle 56:keep the requirements specification readable
#### 保证需求文档是可读的
需求文档需要让大部分人和组织都能读懂，比如用户，客户，市场人员，设计师 ，测试者等。并且让这些人都要充分理解系统的功能。创建多版本的需求文档以给不同的人，最大的挑战就是要保持他们之间的版本一致。一个有效的方法是，始终维护自然语言描述的版本，并在上面加上其他参与方所需要的描述维度。

#### 思考
**还是那句话，要考虑到文档的受众，不能想当然的以为自己能看懂就好，我们日常写PPT时也有这种问题**

### principle 57:specify reliability specifically
#### 明确可靠性
软件的可靠性是比较难以定义的，不要把可靠性定义的不明确，比如可靠性99%这种，要明确到，从请求数量上失败发生的概率，系统down调的时间百分比等。

#### 思考
**除了功能要写到需求里，性能也要写到，有些东西只有功能能用，性能不满足，同样无法应用。如果写了性能的需求，那就要写明确。比如不能只写平均响应时间，还要写99分位，99.9分位要到多少，作为客户量巨大的互联网公司，小概率上的极端情况同样会影响到不少用户。**

### principle 58:specify when environment  violates “acceptable” behavior
#### 明确当环境变的可用这行为的含义
需求文档通常会写系统工作的环境。这个环境的定义会影响到设计，开发人员。当环境和预期不一样时部署会有什么问题？当环境变化，报告流量超过当初设计的预期时。不能让系统crash，出错，或者静默的忽略额外的流量。要在系统定义中明确环境不是预期了会有怎样的效果。

#### 思考
**作为公司企业，一个简单的方法就是保证自己的服务器，环境是相同的，线上线下都一样。但是作为用户侧的环境就要通过广泛的测试来保证了。流量的增长也可以看作是一种环境的变化。我们应该不能预先知道所有的非预期情况，所以必要时还是要打出错日志，报错误信息的。当然文档中写明白最好，比如“除以0的行为是未定义的”。**

### principle 59:self-destruct tbd's(To Be Determined)
#### 干掉需求文档中的"后续确定"
需求文档中通常有许多“后续确定”的地方，这样的文档显然是不完善的。当然这也是有意义的，就是当文档的精确度对基础设计没有什么太大影响的时候。当写一个TBD时就要写上注释，谁后续在何时会补充完整他。

#### 思考
**合理的写TO DO，每次邮件明确TODO由谁，在何时来完成。同时要有后续检查的机制，这一点很多时候往往做不到，没有监督，这些TODO后续就费了，也让这套机制整体不Work。导致把复杂的问题都往后抛，所以也不能滥用，有的会议上就是为了确定问题的，不能再TODO了。**

### principle 60:store requirements in a Databases
#### 把需求文档写到数据库中
需求文档是复杂和易变的，存在数据库中便于改变，记录每个需求的特征。比如保存每个需求功能的TAG，便于检索。需求的内容，和其他需求功能的联系，优先级，预期的变动。在那个版本开发了该需求等等。理想情况下需求文档就是数据库的dump。

#### 思考
**目前公司中的需求都是一个个的word，都要靠自己管理，这方面由于每个需求拆的比较小，所以往往也不是痛点。现在也已经和一些工作流的软件进行了结合，但是感觉需求本身确实可以做一个管理系统，明确的知道那一次上线，上了什么功能。**

## chapter 4: design principles 设计原则
设计是以下系列活动的概括，包括，1.设计满足需求的软件的架构2.明确每个架构中软件模块的算法。架构又包含了软件中所有模块是如何交互，如何互相组成，模块中的对象是如何创建和销毁的。设计阶段最终的产品就是设计文档。

### principle 61:transition from requirements to design is not easy
#### 把需求转化为设计并非易事
需求工程的最终是形成需求说明，描述整个系统的行为，设计的第一步是总结出一个理想的软件架构。并没有原因能够说明为什么在软件领域把需求转变为设计是那么的不容易，比起其他的工程学科。设计是困难的，从一个外部的视角转化为一个内部的合理设计是一个困难的问题。有些方法声称这种转变是容易的，通过给出一些建议，比如采用需求文档中的架构作为软件的架构。有三个原因导致设计的困难。
1.在需求的时候并没有考虑选用怎样的理想的设计，所以，你就不能把需求的设计当作最终的设计。
2.即使在需求时，就充分考虑到了设计，并且经过分析选择了最好的设计。公司也不可能支付这么大的代价在前期全局的设计上，而这个过程又在基础的需求分析，决定是买还是开发，开发预算评估这些过程之前。
3.这个方法假设了有一些架构适合所有的应用，这显然是不正确的。

#### 思考
**之前的准则中提到，不要在需求时就考虑设计，这里也说明了，提前考虑设计代价太大。如果经过需求分析，开发预算的预估后发现，买一个比开发一个代价更低，那么在这之前做设计就完全没有必要了。那反过来，如果一开始就明确了必须要进行自己开发，那么此时可不可以就在需求分析时就考虑好设计呢？我认为还是可以的，比如要开发一个检索引擎，需求中有一点说明了要求实效性，因此设计时就可以考虑lambda的架构**

### principle 62:trace design to requirements
#### 把设计和需求对应起来
设计时需要知道那一部分需求是由那个模块完成的，当选择软件的架构时，很重要的一点就是要保证需求被完全覆盖。当部署后，如果发现了一处失败，维护人员可以快速的隔离这个包含错误的模块。当维护时一个模块被修复了，维护人员也需要知道它对其他模块的影响。可以用一个巨大的表格来记录模块和需求之间的关系。有人会说这种表格难以维护，我则觉得你需要这个表格帮助你设计和维护系统，没有它很容易升级错误，花费额外的时间代价去维护它。创建这个表格则依赖于你对每一个需求的精准识别。

#### 思考
**我们目前的系统，大多数很多很多模块，共同支撑了一个产品上的需求，导致一旦产品上除了错误，就很难排查是那个模块导致的错误。还是应该对模块的功能再细分，明确模块自己的需求，采用分治的思想。作者提到的这个大表格固然好，但是缺失难以维护，看作者的意思就是，就算困难也要硬维护，不然出了问题代价更大。**

### principle 63:evaluate alternatives
#### 评估候选方案
所有工程中的一个重要环节就是分析众多的方案，并最终选择其中一个。在需求明确后，你必须要检查这些架构和算法，看那个可用。你不会采取一个架构仅仅是因为需求文档中是按这个架构写的。毕竟，架构的选择要考虑到系统全部行为的最优化。并且要满足所有的需求。举例，我们通常挑选架构是为了最优化吞吐量，响应时间，可修改性，安全，可用性等等，并同时满足需求。最好的方法就是枚举所有的软件架构，然后分析他们，选择一个最好的。一些软件设计方法会导致特定的架构，因此为了有不同的架构就要考虑用多种不同的设计方法。

#### 思考
**我们往往会用我们擅长的架构来处理遇到的新问题，其实可以多考虑考虑是否有别的架构适合这个问题，会不会效果更好。对于架构的评估和选择，还是要看除了满足需求外，最大的痛点是什么，一般都是为了解决性能问题。但是可维护性也很重要。**

### principle 64:design without  documentation is not design
#### 没有文档的设计不是设计
完成了设计，却没有落实到图纸上，就像小说家说完成了小说而没有落实到文字上。设计是一种选择，抽象，并且记录一个近似的架构和算法到纸上或其他媒介上的工作。

#### 思考
**写下来有助于明确，经常遇到讨论一个架构，一个问题，然后大家都认为讨论清楚了，但是并没有落实到文字上，导致最终开发的时候还是有问题**

### principle 65:encapsulate
#### 封装
大多数的软件模块需要隐藏信息，把内部信息封装起来，对其他模块或者软件进行隐藏。这些信息可以是数据结构，数据内容，算法，硬件等。这种信息的隐藏，有助于模块互相独立，一旦出现问题便于定位。因为一个信息被一个模块隐藏，其他模块是不知道的，一旦该信息相关的处理出错，那么只能是该模块有问题。封装代表着一些列需要隐藏信息的规则。比如在面向对象中通常会封装数据和方法在每个对象中，其他对象只能通过请求这些方法影响其中的数据。

#### 思考
**封装是一个在软件架构设计时就要考虑的事了，而不能只在开发具体的代码时考虑。**

### principle 66:don't reinvent the wheel
#### 不要重复发明轮子
当电子工程师设计电路板时，会挑选一个最相近的电路板。建筑师会用定制好的门，窗。这些都叫做‘工程’，软件工程师通常会一遍一遍的重复造轮子。软件工程师通常称呼这叫重用，而不叫工程。

#### 思考
**写软件本身还是为了解决现实中的问题，应该以满足解决问题为目标，怎样又快又好的达成目标，而不要陷入磨练技巧中。**

### principle 67:keep it simple
#### 保持简单
简单的架构和算法有助于达到高可维护性。当把一个软件分解为几个模块的时候，要记得，人类通常很难一次理解超过7样事务。构建软件有两种方法一种是使他如此简单以至于明显没有缺陷，另一种是使他如此复杂以至于没有明显的缺陷。

#### 思考
**简单可依赖，奥卡姆剃刀原则。但同时又和之前的原则、一个结论：通常复杂的问题没有简单的解法，或者不存在简单的解法适合所有问题。相悖。这里的意思应该就是尽量，能简单就简单，有时候针对复杂的问题，一个复杂的方案也是简单的。**

### principle 68:avoid numerous special cases
#### 避免特殊逻辑
当设计算法时，你会考虑到特殊情况。特殊情况会让算法里有特出的处理逻辑。每一个特殊逻辑又会导致调试，修改，维护和更新算法变的困难。如果发现又太多的这种特殊逻辑，大概率是选择了一个不合适的算法。重新设计算法。

#### 思考
**我们的业务中，由于产品需要，经常会有非常多的特殊逻辑。这种情况是否属于作者说的呢？我觉得这种业务特殊逻辑本身就是业务，他的存在就是他的目的。应该不属于。**

### principle 69:minimize intellectual distance
#### 最小化知识距离
 intellectual distance是说现实问题和计算机的解决方案之间的距离，这个距离越短，越容易运维软件。为了满足这个条件，软件的结构要和现实近似。比如面向对象设计方法就是最小化这个距离的一个好的方法。但是现实世界的结构往往在不同的人眼中是不同的。

#### 思考
**如果说软件是现实的抽象，那么如何还能保证是结构相似的呢？**

### principle 70:keep design under intellectual control
#### 保持设计在知识的控制下
如果设计被建立，并且文档化，以至于其创造者和维护者都能很好的理解这个设计，那么就说它在intellectual的掌控下。这种设计的一个必要的属性是，这种设计要分等级，并且从多个视角构建。分层级使得理解的人可以先抽象了解设计，然后逐步深入细节。每一个层级的模块的不同部分应该用不同的视角描述。每一个组建都要是简单优雅的。

#### 思考
**分层次的设计，值得学习，最好从书写上就能分层级的写。还有就是要考虑受众。**

### principle 71:maintain conceptual integrity
#### 维护概念上的完整性
概念的完整性是高质量设计的重要属性。概念完整意味着采用了有限的设计格式，并且他们是统一的。设计格式包括了模块的调用关系，错误处理，交互，数据结构，状态机制，文档标准等。当设计完成时，需要看起来像是一个人完成的。设计阶段会有很多诱惑导致偏离原来的设计格式，但如果是为了更优雅，更统一，满足系统性能，那就可以，如果是为了满足个人的自尊，那就不能牺牲整体的完整性。

#### 思考
**代码要有编码规范，写设计，写文档也要这样。**

### principle 72:conceptual errors are more significant than syntactic errors
#### 概念上的错误会比其语法上的错误更严重
当开发软件时，无论是写需求文档，设计文档，代码还有测试，我们都会花很多功夫在修改语法的错误。这是很好的，但是开发软件真正的困难却来自于概念的错误。大多数开发人员花很多时间在查找和修改语法错误，因为当发现这些愚蠢的错误时甚至会令你发笑。相对的，开发人员经常会感觉到对概念错误的无能为力。无论你多优秀，都会犯概念性的错误。要及时发现他们。在开发的不同环节问自己重要的问题。需求分析时问自己。这是用户想要的么？在设计时问，这个架构在高负载下还能正确的工作么？这个算法在所有的情况下都正确么？在编码时问，这个代码是我想要的么？这个代码正确实现了算法么？测试时，这个测试的执行能让我确定任何功能都是正确的么？

#### 思考
**这里概念上的错误，我理解是包含了非语法上的，逻辑错误，设计错误等，而语法的错误我们可以通过反复检查，配合IDE检查出来，但是这种逻辑，思想上的错误却是我们本身难以认识到的，如果认识不到就更谈不上修改，这也正是一些bug的来源。作者通过问问题的方式，相当于一个checklist，防止自己的思虑不全。每次发现新的问题，都可以记录下来，下次增加对应的问题，这样每次开发后，都对这个列表挨个确认，以防止遗漏**

### principle 73:use coupling and cohesion
#### 使用耦合和内聚
耦合和内聚在1970年被定义，他们至今都是最好的方式，去衡量软件系统内在的可维护性和适应性。简单的说，耦合是两个软件模块怎么相互关联的程度。内聚是一个软件模块中不同函数之间的关联的程度。我们都需要低耦合高的内聚。高的耦合意味着，当我们当我们修改一个模块时，也需要修改其他的模块。低内聚意味着难以隔离错误，难以扩展新的需求。大多数软件开发书都会写这些设计原则，需要在软件中使用他们。

#### 思考
**如果内聚不够，一个功能会有多个模块，多个类共同支持，那一旦出问题，这些地方都要修改。这一点也和耦合是对应的。功能散落在各处，意味着有新的需求要更新功能时，很多地方都要修改，逻辑会越来越复杂，影响也会越来越大。这些原理说起来容易，但是实践中，很难第一次设计就是完美的，需要反复重构，由于项目紧张，我们往往会觉得先实现了再说，将来再重构，这样代价会越来越大。由于工作的性质，大家往往还都倾向于给后来的人埋这个坑。作为项目的管理者，或者公司的管理者要有长远的眼光。**

### principle 74:design for change
#### 面向变化设计
在软件开发中，我们不能考虑到所有的错误，新的需求，或者早起沟通误解带来的问题。所有的这些都会导致设计的更改。进一步即使是基础设计后，并且交付产品后，依然会有新的需求出现。所有的这些都意味着你选择的架构，模块，以及技术要能适应变化，不断的被修改。为了适应变化，一个设计应该满足：
模块化，软件应该由独立的模块组成，每个模块便于升级更新，而对其他模块影响尽量小
可移植性，移植到不同的主机，不同的操作系统上
可扩展性，要能适应新的需求
有最小的知识距离
保持设计在知识的控制下
概念完整性

#### 思考
**唯有变化才是永恒不变的，但是也不要过度设计。前三个点好理解，后面归纳为是设计要尽可能的简单可用，并且保证文档的齐全**

### principle 75:design for maintenance
#### 面向可维护的设计
最大的设计风险就是软件的后期维护，而这一点并没有成为软件开发的标准。设计师必须要对选择的软件架构负责。架构对系统的性能会有深远的影响，同样也会对最终产品的维护产生深远影响。相比于算法或代码，架构对维护的影响更大。

#### 思考
**软件开发中运维的时间占了很大一部分，前期省的一点儿时间，后面可能要加倍还债。好的架构才能让后续的维护变的容易，大概这就是为什么架构师值钱的原因吧，前期一个好的决策能省去后期大量的成本。**

### principle 76:design for errors
#### 面向容错设计
无论再怎么努力，软件都会有错误。要优化设计，使得：
1.错误不会是不被发现的。
2.错误容易发现和检测
3.软件部署后，如果还有遗留的错误，那么要么其不重要，要么就是正常的流程中考虑到了该错误的处理。
这些鲁棒性的设计通常很难包含在设计中，以下方法或许有用：
1.不要跳过任何一个case，比如一个变量可能有四个取值，不要检查了3个时就觉得第4个OK，要检查，并且设计好错误处理
2.要预测尽可能多的“不可能”条件，并且开发策略修复他们
3.为了评估会导致灾难的错误条件，可以操作错误树的方式分析，预测可能不安全的错误条件

#### 思考
**设计时通常只会考虑特别明显的错误，一般不会考虑的那么细。这里要注意，并且把错误的处理也当作架构的一部分。**

### principle 77:build generality into software
#### 软件要有通用性
通用型的软件更难设计，通常执行也会更慢一点儿。在复杂系统中很好用，因为一个相似的函数会出现在多个地方。适用于其他不需要修改的系统。减少维护成本，因为相似组件减少了。在分解一个系统到子子系统时，保持通用型的敏感度。如果相似函数多个地方使用，就要用一个通用函数替代。

#### 思考
**尽量不要写重复的代码，为此如C++，使用宏有时候也可以。通用性最大的优点就是便于维护，适合更新。代码通用性，再网上就是函数，模块，系统的通用性。这其中要求有抽象能力，同时越往上也要越注意不要过度设计，过度设计。**

### principle 78:build flexibility into software
#### 软件要有灵活性
如果一个组件有灵活性，那就意味着其容易修改，以用在另一个场景。灵活性提升了设计的复杂度。灵活的组件，运行时比通用软件高校。在不同的应用中重用度也更高。

#### 思考
**前面的通用会导致模块更加重，而灵活讲究一个轻量。**

### principle 86:

## Chapter 2 编码原则 Coding Principles
编码包括把设计的算法翻译为编程语言，再把程序翻译为可执行语言。
### principle 87:avoid tricks
#### 避免Trick的实现
很多程序员会写trick的程序，虽然写的函数能正常工作，但是看起来不够清晰，有时候实现的函数还有副作用，很多程序员把其称呼为聪明的做法，其实是很傻的。有许多途径解释为什么我们会用trick的方法：1.程序员非常聪明，并且想要展示这种聪明。2.维护代码的人发现了一段trick的代码如何工作后，不但会认为原来的程序员很聪明，而且还会觉得自己和他都很聪明。3.工作的安全性（别人看不懂就能抱住自己的工作？或者专门不让别人看懂？）要遵从一个底线，告诉世界你多聪明要从避免tricky的代码开始。

#### 思考
**trick还有细节的原因，可能就是1.业务确实复杂，业务本身就trick（举例，有时候注释上会写PM要求这么干。。）2.没有良好的设计，和重构的能力，导致每次有新的需求时，反复修修补补，代码看起来就越来月trick，若果有好的设计，就可以避免。3.有时一个系统有一个良好的设计，但是你看不懂她时，就在其上面修改，于是改的就很trick（举例，报表引擎可以通过配置来声明算子，定义一种计算方法，还有应用的列，时机等，由于自己不知道，于是继承了一个原来的类，在其中开多个口子去该，实现的就很trick）4.有时候为了性能考虑，会用一些省略，近似的做法，这种省略和近似由于逻辑上通常没那么直观，导致会有trick的感觉，这种我认为是一种聪明的表现，但是还是应该通过注释解释清楚你为什么这么做。总而言之，代码是写给人看的，让别人看懂，可以修改，才是最聪明的做法，不然别人改不了，还要问你，这不是徒添烦恼，聪明人不会这么干的。**

### principle 88:avoid global variables
#### 避免全局变量
使用方便，但是错误不好定位，任意地方都可能修改，面向对象的思想，对象包含数据，其他人通过对象的方法，来改变数据。如果通过传递参数的形式改变数据时，参数过于的多，很可能是设计问题。

#### 思考
**还是有折衷的，我们的很多C++程序中，都还是会用全局的变量，比如全局的配置等。有时候处于多线程初始化的考虑。可以让全局的变量，数据也在一个全局对象中，不过由于namespace的存在，这个全局一般最多在自己模块中，数千行左右，通常不会扩散到其他引入该模块的模块中。**

### principle 89:write to read top-down
#### 从上倒下的写和读
人都是从上到下阅读，写程序是给人看的，也要如此，1.包括一个详细的说明在程序最前面，说明目的和使用方法。2.说明额外的存储，局部变量，算法。在最上面3.使用结构化的程序构建，层次感利于阅读。

#### 思考
**可以考虑，把分散在整个代码中的注释，给提取出来，如算法流程，目的等，一起在前面交代了。这样先总后分，阅读的人的思路更清晰。**

### principle 90:avoid side-effect
#### 避免副作用
副作用指的是过程中，不仅完成了其主要目的，也做了一些其他的处理，这些处理在过程外其实是不可见的。副作用导致了很多软件错误，这些错误往往隐藏很深，除非出了错误，否则难以发现。

#### 思考
**保证一个函数，只完成一个功能，单一共嫩原则，就能最大程度的减少副作用**

### principle 91:use meaningful names
#### 使用有意义的名称
名称起的短，需要写注释来解释，反而需要打更多的字

#### 思考

### principle 92:write programs for people first
#### 写程序首先是为了让人看

### principle 93:use optimal data structures
#### 使用最优的数据结构
数据结构，和程序利用数据的结构是息息相关的。如果使用了正确的数据结构，算法或者流程代码就容易写，容易读，容易维护。当写程序时需要先组织好算法和数据结构。可以先尝试两三种不同的组合，从中选择最好的。把数据结构包装到一个模块中，这样后续如果找到了更好的数据结构就可以方便替换。

#### 思考
**从一开始就知道，自己不可能第一次就写出最优的，这样就能预留好后续改变的可能。**

### principle 94: get it right before you make it faster
#### 先保证正确，再谈性能

### principle 95: comment before you finalize your code
#### 写代码前先写注释
给自己的代码增加注释，便于调试，测试，维护。调试软件时，会发现错误，这个错误要么是把算法翻译成代码时带来的错误，要么是算法本身的错误，前者需要修改代码，不改注释，后者两者都需要修改，如果没有注释，怎么能发现算法错误？

#### 思考
**和代码简洁之道里说的，尽量不写注释。没有注释，一样可以发现算法错误吧，这部分不是很理解作者的逻辑，可能是说注释会比代码看起来更易懂些。**

### principle 96: document before you start coding
#### 写代码前先写文档

#### 思考
**通常项目刚开始时，我们还能保证先写文档，但是随着项目的进展，在开发中，流程和算法逐步的会改变，此时文档就很难跟着改变了。怎么办？1.每次变动时记录一个log，一周后，把这些log统一再整理到文档。2.把要改动的地方攒一批，然后先写文档，进行review，再开发，此时有可能有些改变就不需要做了，不过显然效率更低一些。**

### principle 97: hand-execute every component
#### 手工执行每一个模块
每一个模块都用测试用例，手动的执行。功能隔离，加上完备的测试，能在后续出bug时，帮助定位问题，解决大量时间

### principle 98: inspect code
#### 审查代码
解决大量的测试时间

### principle 99: you can use unstructured languages
#### 可以使用非结构化的语言

### principle 100: structured code is not necessary good code
#### 结构化的代码不是好代码的必要条件

### principle 101: don't nest too deep
#### 不要嵌套太深
人的理解能力有限，只能记住固定的量。

### principle 102: use appropriate languages
#### 使用恰当的编程语言
从高性能，快速部署，低维护成本，程序自身算法数据结构特性，团队现有技术积累和客户要求，这几个角度考量使用什么语言

### principle 103: programming languages is not an excuse
#### 编程语言不应该成为借口
无论选择什么编程语言，都可以实现高质量的程序，作为一个好的程序员应该在用任何语言的时候都是好的程序员，选择了不利的编程语言，最多只能增加一点儿开发的难度，仅此而已。

### principle 104: language knowledge is not so important
#### 编程语言的知识并非那么重要
好的程序员理解高质量程序的概念，而非仅仅是语言层级的语法和语义

#### 思考
所以作为程序员不用纠结要学那个语言，那个语言都要学，随便找一个开始学，然后精通，然后理解编程的思想，软件设计的方法等，这些东西是可以用在所有语言上的。

### principle 105: format your programs
#### 程序的书写要有格式

### principle 106: don't code too soon
#### 不要写的过快
写之前要保证有稳固的需求和设计文档的基础。像盖一座建筑一样，地基很重要。

## Testing principles
#### 测试原则

### principle 107: trace tests to requirements
#### 在需求中追踪需求
重要的是明确那个测试是针对那个需求，1.需要知道是否所有的需求都被测试到了。2.测试时知道当前那个功能正在被检查也很重要。需求有优先级，测试也针对的有优先级，可以通过一个表格，行的是所有的测试，列是所有的需求，然后每个一个格子，就表示这个测试是否和需求有关。这就要求需求是独立唯一的。

#### 思考

### principle 119: the big bang theory does not apply
#### 大爆炸效应并不适用
即使要赶工期，也不能把所有的未测试部分合在一起，一起做集成测试。这样会增加更多额外的时间。

#### 思考

### principle 124: instrument your software
#### 校准你的软件
测试软件时，发现软件为何出错是很困难的。一个发现原因的方法是，校准软件。在软件中增加特殊的指令，跟踪调用，变量，及加日志。

#### 思考
日志调试法

## charpter7: Management principles
#### 管理原则
管理包括：计划，控制，监控，报告所有工程行为和软件开发活动

### principle 127:Good management is more important than good technology
#### 好的管理胜过好的技术
好的管理，激励人们做到他们最好的成都，而坏的管理浇灭激情。所有好的技术都无法弥补不好的管理。而好的管理总是能产生好的结果，即使在缺乏下资源的条件下。成功的软件不会由于他们有好的处理器或者攻击而成功。大多数成功是来自远优秀的管理和优秀的市场。
作为一个经理，你有责任做到最好的自己。这里没有一个常见的“正确”的管理风格。管理风格必须适应不同的场景。一个不是很少见的情况是，一个成功的领导者在有的情况下是一个专断的独裁者，几分钟后又是一个听取各种意见的领导。有些管理风格是先天的，有些是可以学会的。如果需要读一些书，或者参加一个短期的课程去学习管理风格。

#### 思考
有好的产品和管理，没有技术也可以找外包先去做，做好了不愁招人。

### principle 128: use appropriate solutions
#### 采用适当的方案
一个技术问题需要一个技术方案。一个管理问题需要一个管理方案。一个政策问题需要一个政策方案。不要试图在一个问题上采用不恰当的方案。

#### 思考
不要试图用技术，去掩盖管理上的问题。

### principle 129: don't believe everything you read
#### 不要相信任何你读到的东西
作为一个通用的原则，人们通常会相信某种哲学，然后去找数据支持这个观点，而丢掉那些不支持这个观点的数据。一个人试图说服其他人时也会采用支持他的数据而非不支持的数据。当你读到，“使用方法X，你也可以达到93%的效率提升。”这个方法或许的确能达到这样的效果。但是它更有可能时特例的，在大多数项目上可能远达不到这样令人瞩目的效果。而有些项目使用X方法甚至会带来副作用。

#### 思考
要对别人说的保持怀疑，工作中别人说的，交接的同事说的，书本上的权威说的。

### principle 130: understand the customers priorities
#### 了解客户的属性
有很大的可能性，客户宁愿要90%的功能延期，以换来10%的功能暗示交付。这个原则8的推论会有点儿震惊，但是会恰好适合这种情况。
如果你正在和客户交流，你可以肯定你知道他们的特征。这可以简单的记录在需求说明中。但是真正的挑战是了解每一个可能转变的属性。明确的额说，你必须要了解到客户说的“必要” ”可取的“ ”可选的“，他们真的会满意，如果系统没有实现一个他们说的“可取的” ”可选的“ 需求？

#### 思考
客户是人，要从人性的角度上去考虑

### principle 131:people are the key sucess
#### 人才是成功的关键
那些具有高超技艺，并且有适当的经验，天赋和训练的人，才是在预算范围内准时生产出满足客户需要的软件的关键。正确的人即使用低效的工具，语言或者流程也能成功，而错误的人，使用合适的工具流程，语言也可能失败。根据COCOCMO，最优秀的人的效率是其他人的4倍。如果最优秀的人花费4被的薪水，你不赚不赔，最终获得了更好的产品。如果他们要的薪水更少些，那你就获得了更好的软件同时减少了花销，双赢。
当面试获选员工的时候，要谨记什么都不能代替品质。公司通常会说，“面试了两个人后，x会比y好点儿，但是y也挺好，并且还便宜。”你不会有一个组织里面全是超级明星，但是除非你已经有了过多的明星，否则还要是果断的雇他们。

#### 思考
和优秀的人合作效率也会很高，出问题的概率会大大想讲，比如合作的人一个不靠谱，把本来正确的当作错误的，于是你会花费好长时间修复不存在的错误，浪费大量时间。

### principle 132:A few good people are better than many less skilled people
#### 少数的优秀员工也胜过许多技术不行的人
紧跟原则131，你总是应该雇佣最好的工程师。这个原则说到，你最好在一个重要的任务上安排少数优秀的有经验的工程师，而非许多没有经验的人。另一方面，你也不应该太依赖这少出的几个人，如果他们离职了呢？最好的建议是要正确的混合不同的人在一个项目上，而避免走极端（全分配几个优秀的人，或全都是庸才）

#### 思考
体现出管理腹黑的一面，管理时人也是风险的一部分，和软件会出的错误一样，都要有容错的考虑。一方面避免重要的人恃才傲物，一方面也能让普通人跟着优秀的人学习，从而成长为优秀的人。这势必要牺牲一些效率，但是长期看是有价值的。所以破解的事情找优秀的人攻坚，项目平稳后，加入普通的人。

### principle 133: listen to your people
#### 倾听你手下的人
你必须要相信为你工作的人。如果他们不值得信任，或者你不信任他们，那你的项目会失败。如果他们不信任你，你的项目也会失败。你手下的人能最快的发现你不信任他们就像你发现你的老板不信任你时。
信任的第一个原则就是倾听。有很多机会去倾听你手下的人。当他们当你办公室告诉你一个问题时，当你要从他们获取软件开发的预估时，当你他们周围走动式管理时。无论合适你的员工和你交流时，仔细聆听。他们给你说的一定是他们认为重要的事情，否则他们不会告诉你。有很多方法能告诉他们你在专心听，比如眼神交流，身体语言，复述你认为你听到的意思，问合适的问题去获取更多的信息，等等。

#### 思考
都说要信任，如何信任呢？倾听

### principle 134: trust your people
#### 信任你手下的人
信任是相互的，相互的信任是成功管理的关键。当恶人的机会比当好人的机会要多的多，所以一定要尽可能的利用机会当好人。

### principle 135: expect excellence
#### 期求优秀
对员工期待高，他们会表看的更好。有很多方法可以体现出你期望优秀。比如成为榜样，给员工提供教育上的鼓励，从而让他们自己达到最好。给最好的奖励，如果失败了帮他们在内部转岗，或者帮他们在外面找个工作。不能让错误的人待在不合适位置，但是开出它要体现出怜悯。低效的人待在你的团队力，会导致产品质量下降，同时会让其他雇员也觉得低效是可以的。

### principle 136: communication skills are essential
####  沟通技巧是必要的
在招人时不要低估团队合作和共同。最好的架构师如果不能交流倾听理解，也会变成一个无用的人。

### principle 137: carry the water
#### 拿点儿水
当员工工作了很长的时间完成一个工作，你也应该工作同样的时常。员工会更愿意努力的工作如何他们知道他们和你的处境相同。作出一种为员工在工作的角色。如果你无法帮忙在工程开发上，也要让员工只能你在帮忙干别的事，比如定个披萨，拿点水，无论什么他们需要的。可以在午夜给他们定个披萨给他们惊喜。

#### 思考
到手的工资，钱都是数字，有时候远不如一顿鸡翅，一个蛋糕带来的犒劳和辛福感。一方面是实物的帮助，另一方面也要有语言上的鼓励和激励。
但是也会有低效，如果一个人干活，其他们都要陪着一起干活么？而明明又插不上手。经理来就行了？

### principle 138: people are motivated by different things
#### 每个人被激励的动机不同（人各有所好）
这可能是经理最难学的一课。给员工提薪水的激励，可能员工需要的是一台更快的电脑。人是不同的，正向的激励和负向的激励有时候都会生效，但是正向的容易被忽略。一个了解每个人需要什么激励的方法就是倾听。剩下的就只能考试错来发现。不要害怕选择错误的激励，而不去激励。

#### 思考
为什么公司要换mac电脑？也是满足员工的激励需求吧。

### principle 139:keep the office quiet
#### 保持办公室安静
高效的员工和公司有安静和有隐私的办公室。这样不会减少沟通，而会减少无效的打断和噪音。

#### 思考
应该修建隔音的电话间，这样如果需要长期打电话不会打扰他人

### principle 140: people and time are ont interchangeable
#### 人和时间是不能交换的
人月神话，主要因为新人要培训和增大沟通成本

#### 思考
微服务，模块化，标准化接口，等众多的方案，都是为了最大程度的解耦合，从而可以增加人减少月。

### principle 141: there are huge differences among software engineers
####  软件工程师之间有很大的不同
效率很软件的质量不同的人之间差别很大

### principle 142:you can optimize whatever you want
#### 你能够优化你想要的
想要达到质量上某一个方面很优秀，势必要牺牲其他方面。如果你告诉你的人性能，质量，用户界面等一样重要，那么没有一个会被优化。如果只告诉他们一两项重要，其他不重要，那么重要的会被优化。如果有优先级列表，优先级列表可能不适用于项目的所有情况。软件的开发中一直在做权衡，不同的权衡。和员工一起工作，让他们明白你的高优目标，你的客户。

### principle 143:collect data unobtrusively
#### 不显眼的收集数据
数据对应预估花费，评估项目状态已经管理决策的效果等是很有用的。另一方面数据收集是强加于人的工作，比如需要软件工程师做额外的工作收集数据，而这是没什么意义的，如果他自己收集自己的开发相关数据。不配合的员工也不会给你正确的数据。最好的收集数据的方法是自动化的，只要可以自动化就自动化。不要让开发人员接入。

#### 思考
一方面开发效率等数据让开发人自己填报，会有偏差，另一方面也会浪费他们的时间。但为了自动化估计也要增加成本，比如开发时要使用一些数据收集的软件，或者在流程系统中填写信息等。也依靠制度流程的规范。
如果让开发人员自己收集新上线的项目的效果，统计的口径不同，自然会得出有利于他们的效果。

### principle 144: cost per line of code is not useful
#### 每行代码的花费这个数据没意义

### principle 145:there is no perfect way to measure productivity
#### 没有完美的方法去衡量效率
两种方法，源代码行数每月，功能点数每月，都有问题。功能点的复杂程度是不同的。要接受不存在完美方案的事实。使用效率衡量和预算预估模型去验证你的直觉和经验。不要仅仅依赖他们当作你唯一的方法。

#### 思考
那工作中我们常设置的一个目标提高研发效率，运维效率等。该如何衡量呢？由于存在问题，相当于存在benchmark，看有没有提升还是比较容易的。

### principle 146:tailor cost estimation methods
#### 裁剪花费预估的方法
商业上有很多预算评估的方法，都需要从大量完成的项目上收集数据。为了能用他们更精确的预估你的项目应该要裁剪模型以适应你的员工和项目。

### principle 147:dont set unrealistic dealines
#### 不要设置不切合实际的截止日期
不切合实际的截止日期侵蚀斗志，不信任你，从而更达不到目标。大部分项目都会超预算，超排期，但是完成的好。为了排期很可能会缩减质量。这并不是员工和管理者的不才的原因，而往往是因为之前错误的预估导致的。

### principle 148:avoid the impossible
#### 避免不可能
从需求文档到交付产品是有最小时间限度的，避免设定不可能的排期目标

### principle 149:know before you count
#### 计算之前要先知道
当你要计算任何事情的时候，你都要先知道一些事情。很多时候人们不知道在计算什么东西。要寻找自己的度量方法，

### principle 150:collect productivity data
#### 收集生产效率数据
预算模型要被裁剪适配到你的工作环境，但是你必须要收集到足够细节的数据，从过往的项目中。今天有借口做不了准确的预估，明天呢？所以要从今天起开始收集数据。少部分被正确收集，模型化，解释化的数据胜过收集一大堆没有上述属性的数据。

### principle 151:dont forget team productivity
#### 别忘了团队效率
个人效率评估有许多方法。个人效率的最高不一定意味着团腿效率最高。篮球队，队员如果想要个人效率最优，只要不断的投篮就可以了，但这样显然队伍会输球。有两个经验：第一，不同的效率衡量方法适合不同的人。第二，记录团队整体的努力结果，通过记录这样的事情，比如团队的能力去解决突出的问题，按照问题的难度，每个问题解决的时间。

#### 思考
短期效率高，是不是一定意味着长期效率也高？团队解决问题的效率不是也和个人有关么？大多数问题很少配合，还是会落到一个人身上吧？

### principle 152:loc/pm independent of language
#### loc或pm要是语言无关的
通常我们详细一个程序员能够一个月产出一定数量的代码，而无论用什么语言。但是选择高级的语言效率更好，而且有利于维护。
开始项目时要了解你的工程师会用什么语言，这样你能评估代码行数，从而估计排期。

### principle 153:believe the schedule
#### 相信时间表
一旦时间表建立，资源开始投入，各方都必须要遵守这个时间表。如果工程师不详细时间表是真实的，那他就不会满足时间预期。最好的建议是让工程师指定时间表，这通常不可能。第二好的建议是让工程师参与到功能，时间表和项目取消的权衡中去。只有很少的宁愿项目取消丢掉工作，而不去达到一个严苛的时间表。

### principle 154:a precision crafted cost estimate is not foolproof
#### 精确的成本估算并非万无一失
即使有了好的预算预估，也不一定会正确。有三个原因，一是你，二是假设，三是可能。你的领导力会影响到最终的结果。会有各种你预想不到的情况出现，预估只是一个最大的概率出现的可能，而非一定会是这样。

### principle 155:reassess schedules regularly
#### 定期评估时间表


### principle 156: minor underestimates are not always bad
#### 轻微的低估并不总是坏事。
轻微的延期会导致员工工作更努力追赶进度。领先进度会导致休假，工作时间更短，减少效率。但是切记过犹不及。

### principle 157:allocate appropriate resources
#### 分配合适的资源
如果试图压缩工期和预算，效率会减低，消耗的资源反而更多

### principle 158:plan a project in detail
#### 详细计划一个项目
用PERT记录独立的任务，用GANTT图，里程碑，写文档和代码的标准，每个人分配不同的任务。任务会越来越复杂，需求会越来越多。需要更多的细节。

### principle 159:keep your plan uptodate
#### 保持你的计划实时更新
一个不更新的计划，还不是没有计划。错误的计划会让你以为一起在掌握之中。好的计划要提出风险，有新的时间表，里程碑时都要更新计划。保持一致性。

### principle 160:avoid standing waves
#### 避免驻波？
原则159的一个副作用就是驻波。这种情况下，你总是计划好的变好的策略会在接下来几周出现。这样延期的项目会越来约延期。让项目变好会需要越来越多的资源。波会变得越来越大，而没有采取任何行动。重新指定时间表和计划都是需要行动的，而不是只许诺之后会解决他们。不要认为你只延期了几天，问题就会自己解决。所有的延期项目都是从延期一天开始的。

### principle 161:know the top 10 risks
#### 知道10个最大的风险
作为项目经理有一些经常导致软件失败的风险，下面是一些列举：
* 缺人
* 不现实的时间表
* 不理解需求
* 构建了一个差劲的用户界面
* 试图镀金，但是客户并不需要
* 没有管理需求的变化
* 缺少可以重复利用的组件
* 缺少外部执行的任务
* 差的响应时间
* 试图超过现有计算机技术的能力

### principle 162:understand risks up front
#### 预先了解风险
任何软件都不能够精确的预估，什么地方可能出错。但是的确会有地方出错。在计划的早期列出项目最大的风险，评估每个风险带来的危害，出现的概率，以及克服的可能。项目开始后，构建一个决策树写出所有你可以做的降低风险的事。然后指定计划或者立即执行这些行动。

### principle 163:use an appropriate process model
#### 使用一个合适的进度模型
有很多进度模型会适合软件项目，比如瀑布，原型等等。没有一个模型适合所有的项目和组织，选择不同的模型要参考组织文化，风险意愿，应用领域，需求变化，需求理解程度。
了解你项目的特点，然后选择一个合适模型，并且深刻理解它。

### principle 164: the method wont save you
#### 方法不会拯救你
你可能会听到方法的狂热爱好者说，如果你用的我的方法，问题就会不见。无论是结构化，面向对象的方法，一直在变化，没有万灵药，没有什么企业用以前的方法生产不出高质量的软件，用新方法也难。作为一个经理，要小心那些告诉你用了新方法会大幅提升质量或效率的人。用新方法没什么并没什么错误，如果用之前的方法有问题，要做的是查看问题的源头去解决，而不是换个方法。

#### 思考
要深入问题，发现本质

### principle 165:no secrets for miraculous productivity increases
#### 没有能奇迹般提升效率的秘密
这个产业充满了销售人员，试图用新的技术或者工具去减少研发费用。我们在会议上经常能听到经理人们说提升了50%，100%的效率，通过使用什么工具，语言，或者方法。不要相信它！软件行业的效率提升是中等的，每年3-5%。不要削减，比如需求工程师，等其他阶段。应用新工具方法会减少一些预算，但是如果不清楚预算削减的如何影响了客户满意度，那么削减预算就是没意义的。

#### 思考
提升软件质量，性能也是这样，没有什么厉害的架构之类的，一用就大幅提升性能的，很多时候还是在小的问题上，编程细节上解决问题。

### principle 166: know what progress means
#### 知道研发流程意味着什么
不要单独看预算消耗低于预期，时间进度领先预期这些指标，要结合一起看

### principle 167:manage by variance
#### 管理差异
首先，管理项目不可能没有有一个详细的计划，有了计划就要及时更新。然后你的职责是依靠这个计划去管理项目。报告项目进度时只用报告现实和计划不一致的地方。很多经理花大量时间汇报我们目前做的如何好。这样才能让资源和注意力集中在问题上。

### principle 168:dont overstrain your hardware
#### 不要过度劳累你的硬件
研究发现你使用到了90%的内存，CPU，软件的研发费用会double，95%时三倍。要控制营销的消耗在其他项目中。如果内存和CPU容易添加，就不要担心这个原则。如果内存和CPU都很有限制就要提前留足研发排期。

### principle 169:be optimistic about hardware evolution
#### 对硬件的升级保持乐观
硬件的发展会超出你的预期

### principle 170: be pessimistic about software evolution
#### 对软件的发展要保持悲观
预言未来软件会替换到更好的预言，更好的系统，架构上的预言都没有实现过

#### 思考
软件一旦没有问题可以正常运行，是没什么动力去升级它的

### principle 171: the thought that disaster is impossible often leads to disaster
#### 总是认为灾难不会发生往往会导致灾难发生
泰坦尼克原则，过度自信是很多灾难的首要因素。要一开始先研究风险，然后指定计划。你最大的管理风险会在你认为不存在的时候出现

### principle 172:do a project postmortem
#### 要做项目复盘
项目结束要用给项目关键参与者3，4天的时间去分析项目中出现的问题。项目中记录问题，项目后分析问题，从问题中学习，写下之后改进的方法，从而在新项目中做的更好。
