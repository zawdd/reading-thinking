# 软件开发的201条准则
# 201 principles of software development
## Chapter 1 介绍
软件工程需要有别于物理，生物等工程的原则。
原则原理-》技术-》语言-》工具
原则在发展和变化，适用于以前的不一定适合现在。
## Chapter 2 通用原则
### principle 1: Quality is #1
>A customer will not tolerate a product with poor quality, regardless of the definition of quality. Quality must be quantified and mechanisms put into place to motivate and reward its achievement. It may seem politically correct to deliver a product on time, even though its quality is poor, but it is politically correct in the short term only; it is political suicide in the middle and long term. There is no trade-off to be made. The first requirement must be quality. Edward Yourdon suggests that you Just say no”when you’re asked to speed up testing, ignore a few bugs, or code before agreeing on a design or a set of requirements

* 质量是第一位的
即使短期内看，按时上线是政治正确的，但是其牺牲了中长期了利益。对于质量没有什么可权衡了，必须要保证。应该把质量保证做如激励和奖励的机制中去。要say no，当需要跳过测试，忽略bug，在有完整的设计前就开始开发时。
* 思考
**首先，要区分什么是质量问题，为了快速迭代，原型的开发去掉了一些功能，等并不是质量问题。其次，软件中的bug是不可避免的，我们要解决我们发现的问题，但是没发现的问题我们也解决不了，不能认为我们按照了质量工程流程的要求做了该做的，就没有质量问题了，依然要准备好出了质量问题的预案。最后，如果我认为质量还是会有trade off的，如果保证质量的代价，大于出了质量问题的代价，那么或许就不值得了，比如密码学中不需要绝对的安全，只需要破解的代价足够大就可以了，当然显示时间的代价，不是计算机中的时间复杂度那样可以明确量化衡量的，有一些软件的质量问题，比如会造成人死亡，你就无法明确其代价是多少。那日常工作中我们该怎么办呢，预先定好质量保证的方案和流程，广泛进行讨论后通过，然后严格按照流程去执行，不要偷工减料，最大程度的尽人事，然后听天命。**

### principle 2: quality is in the eyes of the beholder
>There is no one definition of software quality. To developers ,it might be an elegant design or elegant code. To users ,who work in stress environments,it might be response time or high capacity. For cost-sensitive projects, it might be low development cost. For some customers, it might be satisfying all their perceived and not-yet-perceived needs. The dilemma is that these may not be all compatible. Optimizing one persons quality might be detrimental to anothers.(This is Weinberg’s”Political Dilemma”principle. )A project must decide on its priorities and articulate them to all parties.

* 质量是旁观者的眼睛
软件质量并没有明确的定义，对于开发者可能是优雅的代码和设计，对于负载压力大的用户意味着高性能的请求响应，对于高预算的项目意味着开发价格更便宜，对于有些客户意味着满足他们的提出的和未提出的需求。困难的是这些无法全部实现，满足一部分人的需求，就会牺牲其他人的需求，一个项目必须要决定它的优先事项，并且告知所有人。
* 思考
**这一步最好在项目开始的时候就进行，把为了满足那一方的利益牺牲了什么利益都讲清楚，比如把压缩工期的可能会导致的质量问题，功能减少问题就提前告知PM，告知经理，如果能够达成一致就继续。凡事都不可能一开始都设计好，出现问题也要即使的反馈，及早的告知有影响的参与方，让他们知道自己的某项预期达不到了，早有准备。根据这本树的原则看，质量应该是最不能被牺牲的一个维度**

### principle 3: productivity and quality are inseparable
>There is a clear relationship between productivity(measured by numbers of widgits–whether they be lines of code or function points–per person month)and quality. The higher the demand for quality, the lower your productivity becomes. The lower the demand for quality, the higher your productivity becomes. The more you emphasize increased productivity, the lower your resulting quality. Bell Labs has found that, to achieve one to two bugs per thousand lines of code, productivities of 150 to 300 lines of code per person-month are common [see Fleckenstein, W,”Challenges in Software Development, ” IEEE Computer, 16, 3(March 1983), Pp 60-64].As attempts are made to drive productivity up ,the density of bugs increases.

* 生产率和质量是不可分开的
生产率和质量是相关的，越要求提升生产率，就会导致质量下降。

* 思考
**也说明效率的提升是有上限的，但是现实中效率的提升和改变是明显可衡量的，而质量则不是，这估计也是导致人们为了效率而牺牲质量的原因**

### principle 4: high quality software is possible
> Although our industry is saturated with examples of software systems that perform poorly, that are full of bugs, or that otherwise fail to satisfy users’ needs, there are counter examples.large-scale software systems can be built with very high quality, but for a steep price tag: on the order of $1000 per line of code. One such example is IBMS on-board flight software for NASAS space shuttle. Totaling approximately three million lines of code,the rigorous software development process resulted in less than one error found per ten thousand lines of code after product release.
>
As a developer, be aware of the techniques that have been demon-strated to increase quality considerably. These include involving the customer(Principle 8), prototyping(to verify requirements prior to full-scale development; Principles 11 through 13), keeping the design simple (Principle 67), inspections(Principle 98), and hiring the best people ( Principles 130 and 131). As a customer, demand excellence but be aware of the high costs involved

* 开发高质量的软件是可能的
尽管现实世界的很多软件系统都质量很低，充满了bug，不能满足需求，但是构建一个高质量的大规模的软件依然是可行的，价格会急剧上升到1000美金一行代码，IBM严格的控制质量，使得一个航天飞机软件代码错误率效益每一万行代码一个bug。作为一个开发者，要知道已经被证明能提高质量的技术，涉及到客户，原型开发，保持简单的设计，检查，雇佣最优秀的额开发人员。作为消费者，要求卓越的质量，但是要考虑到花费。

* 思考
**还是要考虑实现高质量的性价比**

### principle 5:don't try to retrofit quality
>Quality cannot be retrofit into software .This applies to any definition of quality: maintainability, reliability, adaptability, testability, safety, and so on. We have a very difficult time building quality into software during development when we try to. How can we possibly expect to achieve quality when we don’ t try? This is primarily why you must not try to convert a throwaway prototype into a product(Principle 11).

* 不要试图改进质量
软件的质量是不能改进的，这适用于质量的定义是可维护性，稳定性，适应性，可测试性，安全性等。在尝试开发时，很难提升软件的质量。不能期望从一个原型改进成一个产品。

* 思考
**这里的含义应该是质量的保证要在已开始设计时就体现出来，不能像做实验一样，一边实验一边开发，没有规划，没有全盘的设计，此时试图保证质量是不现实的。根据作者的理解，产品的原型应该就是验证想法，可行性的初步版本，后续完整的产品应该从头设计开发，这和目前互联网时代，快速迭代的开发应该是不太相符的，作者的时代是传统软件开发的时代**

### principle 6: poor reliability is worse than poor efficiency
>When software is not efficient, it is generally possible to isolate the sections of the program that consume most of the execution time and redesign or recode them for increased efficiency(Principle 194).Poor reliability is not only more difficult to detect, it is also more difficult to fix.A system’s poor reliability may not become apparent until years after the system is deployed–and it kills somebody.Once the poor reliability manifests itself, it is often difficult to isolate its cause.

* 低的可靠性比低效率更糟糕
当软件的效率不高时，可以隔离这部分低效率的代码，通过重新设计，重构的方法提升其效率。对于低可靠性，不仅更难检测，而且更难修复。低可靠性可能持续数年才能被发现，而且一旦出现问题，也很难去隔离这个他。

* 思考
**可靠性低的修复往往是牵一发而动全身，不像性能效率一样，容易发现瓶颈。正确的基础上谈效率才有意义**

### principle 7:give products to customers early
>No matter how hard you try to learn users’needs during the requirements phase, the most effective means to ascertain their real needs is to give them a product and let them play with it.If you follow a conventional interpretation of the waterfall model, the first delivery of a product to the customer occurs after 99 percent of the development resources are already expended.Thus, the majority of customer feedback on their needs occurs after the resources are expended.Contrast that with an approach, for example, of constructing a quick and dirty prototype early in the development process.Deliver this to the customer, gather feedback, and then write a requirements specification and proceed with a full-scale development.In this scenario, only 5 to 20 percent of the development resources are expended by the time customers experience their first product.f the appropriate features were built into the prototype, the highest-risk user needs will become better known and the final product is more likely to be user-satisfactory.This helps ensure that the remainder of the resources are spent building the right system.

* 尽早的交付产品给客户
无论前期需求分析阶段多么努力的了解客户的需求，都不如给客户一个产品，然后他使用产品，从中发现需求。如果遵循瀑布模型开发，第一次交付给用户时，开发资源的99%已经被耗尽了，此时才能从客户身上得到反馈。于此相反，在开发早起构建一个不完善的原型，然后给客户使用，获取反馈，然后再写需求分析，进行全量的开发。此时第一次交付时只消耗了5%到20%的资源。通过原型验证，发现客户真正需要的功能，这样保证了开发资源都被用在了正确的事情上。

* 思考
**对于互联网产品尤其适用，先用小的代价实现一个效果可能没那么好的版本，然后看消费者的使用情况，然后进一步改进。不过这里有一个问题就是，有可能这个比较差的原型上线后，尝鲜型的使用者用后，由于效果不好就放弃了，即使我们后期改进了一个更好的版本，可能这部分人也不会再使用了，失去了对产品的信任。这样，是不是就需要功能效果完善后再上线了呢？这其中的度是最难把我的**

### principle 8:communicate with customers/users
>Never lose sight of why software is being developed:to satisfy real needs,to solve real problems.The only way to solve real needs is to communicate with those who have the needs.The customer or user is the most important person involved with your project.If you are a commercial developer, talk often with the clients.Keep them involved.Sure, it is easier to develop software in a vacuum, but will the customer like the result?If you’re a producer of shrinkwrap software,”customers”are harder to locate during development.So role-play.Designate three or four individuals in your organization as prospective customers and tap them for ideas that will keep them as customers or make them happy.If you’re a government contractor, talk often with the contracting officers, their technical representatives, and, if possible, the users.People and situations change often in the government.the only way to keep up with the change is communication.Ignoring the changes may make life seem easier in the short term, but the final system will not be useful.

* 和用户交流
永远不要忽视为何进行软件开发，是为满足现实的需求，解决现实的问题。必须要和有问题的人交流才行，用户是项目中最重要的参与者。沟通的目的是为了了解变化，如果忽视变化，短期内生活会变容易，但是长期来看就没效了。如果开发时客户比较难以确定，可以在项目内部指定几个人扮演客户的身份。

* 思考
**互联网项目中，toC产品中还能找一些人调研，使用，但是对于toB产品来说，用户就是一个企业了，就不那么具象了，如何提升其在项目中的参与程度？应该还是要落实到具体企业软件使用的人身上，还有企业的问题和发展诉求。而且目前很多公司都是产品经理，运营人员接触客户较多，作为开发人员反而没怎么直接接触用户，客户的想法通过产品经理传到开发人员那里，可能会有偏差，由于身处项目中的角色不同，开发人员和产品经理看待问题的角度也会不同。**

### principle 9: align incentives for developer and customer
>Projects often fail because customers and developers have different(and perhaps incompatible) goals.For example, take the simple case in which the customer wants features 1, 2, and 3 by a specific date and the developer wants to maximize revenue or profit.To maximize revenue the develper may attempt to build all three features in their entirety even if late.To maximize revenue the develper may attempt to build all three features in their entirety even if late.To help align the two organizations’ goals:
(1)Prioritize requirements (Principle 50)so that developers understand their relative importance,
(2) reward the developer based on the relative priorities(for example, all highpriority requirements must be satisfied, each medium priority requirement earns the developer a small additional bonus of some kind and each low priority requirement satisfied earns a very small bonus),
(3)use strict penalties for late delivery

* 调整开发者和客户的奖励机制
项目会由于客户和开发者的目标不一致而失败，比如客户需要1，2，3个功能在特定的日期，而开发者为了最大的利益会统一开发这个3个功能，即使会延误交付日期。而客户也只能先失去某些功能，直到其他的功能开发完毕。为了对齐两者的目标，1.把需求分优先级，让开发者明白什么是相对重要的；2.就相对的优先级来给开发人员付报酬，比如所有的高优需求必须满足，每个中优需求会给开发人员带来额外的奖励，低优需求带来小的额外奖励；3.对于延期指定严格的惩罚措施

* 思考
**开发者应该把上述为了提高收益而合并开发的事情提前告知客户，争取达成一致，作为条件可以附赠一些低优的功能。开发人员也要有好的设计能力，使得程序有可扩展性，能够适应未来可能有的变化，尤其是后续的变化是目前低优，中优的需求，那么大概率未来可能还是要开发，所以要提前设计好。**

### principle 10:plan to throw one away
>One of the most important critical success factors for a project is whether it is entirely new.Programs that tread on brand new territory(whether it be with respect to application, architecture, interface, or algorithm) rarely work the first time.Fred Brooks, in his Mythical Man Month, makes this perfectly clear with his advice, “Plan to throw one away; you will anyway.”This advice was originally presented by Winston Royce in 1970, when he said one should plan for the first fully deployed system to be the second one created.The first should at least check out the critical design issues and the operational concept.Furthermore Royce recommended that such a prerelease version should be developed with approximately 25 percent of the total system development resources.As a developer of a new custom product, plan to build a series of throwaway prototypes(Principles 11, 12, and 13)before embarking on the full-scale product development.As a commercial high-volume developer expect that your first product version will be able to be modified for a certain period of years, after which it will need to be fully replaced(related Principles 185, 186, 188, and 201).As a maintainer of a product, be aware that you can fiddle with the program just so much before it becomes unstable and must be replaced (see related Principles 186, 191, 195, and 197).

* 计划扔掉一个
项目成功的最重要的一个原因就是这个项目是否是新的。进入全新领域的程序很少能第一次就工作正确。有一句话说到，计划丢掉一个，你迟早还是会拥有的。第一个完全部署的系统应该是由前一个升级来的。第一个版本应该能够检查出设计的问题，以及操作理念的问题。进一步，这个第一个版本应该用25%的总资源来开发。作为一个新的项目的开发人员，应该做好准备丢掉一系列构建的原型。作为一个大的商业软件的开发人员，要保证你的第一个版本能够后面数年被持续修改。作为一个项目的维护人员，在程序变得不稳定，必须被替换之前，你可以对程序做持续的修改。

* 思考
**这里应该要表达的就是原型开发，和程序要有可扩展性，可以持续进化改进。而且第一个原型往往是用来验证的，后续可以扔掉他，在其基础上再做新的。问题在于，一个项目持续几年后，由于人员的变动，代码文档的不健全，导致后面的升级和修改越来越难做，后面的开发人员也不敢对项目进行升级改进了。那么此时该怎么办？如何衡量什么时候该重新做一个新项目替代他，还是继续保持现状，这里当然要衡量两者的代价，可是低价的标准不太好定，基于质量是第一位的，我觉得应该当老的项目由于维护性差出了线上严重问题时，就要考虑替换了，单纯的考虑人力成本，那开发新项目的成本无论何时基本上都会大于修改老项目**

### principle 11:build the right kind of prototype

* 构建正确的原型
有两种原型，需要抛弃的原型和可以进化的原型。可抛弃的原型是快速构架，用来获取客户的反馈，明确需求的。可进化的原型是在严格的质量保证下开发的，给客户用来获取反馈，然后根据需要进行修改，反复迭代直到产品完全满足需求。可抛弃原型的用途是当重点的功能不能被清晰理解，明确时。可进化的原型是重点功能明确，但是其他功能不清晰时。如果大部分功能都不明确那么就需要以进化原型的角度构建一个可抛弃的原型

* 思考
**现代这中可抛弃的原型估计就是设计图或者纯前端就可以搞定了，对于可进化的，即需要持续改进的，就需要保证设计是兼容性强，可以灵活变动的，不然后续的每次修改代价会越来越大，操作中可以每完成几轮迭代后就抽出部分时间，进行代码的重构，保证结构的优雅，便于进一步开发，如果是长期项目，考虑到人员的变动，文档等也要更加完善，以让后面的人可以接手**

### principle 12:build the right features into a prototype

* 在原型中构建正确的功能
当构建一个可抛弃的原型时，应该只开发哪些不清晰的功能。开发哪些明确理解了的功能，不能学到任何东西，并且浪费资源。构建进化原型时则开发哪些被最明确的功能，期望用户通过使用这些功能，让用户决策是否需要附加额外的功能。如果在进化原型中开发了不明确的功能，那么就有可能需要抛弃这个“高质量”原型的风险，浪费资源

* 思考
**商业软件，外包开发时能够明确客户的需求，对于互联网产品，客户有时候是潜在的，并不直到自己的需求，这个需求往往是开发团队自己确定的，开发了原型然后到市场上去实验，此时抛弃这个原型与否的就是市场了**

### principle 13:build throwaway prototypes quickly
* 快速开发可抛弃的原型
开发可抛弃的原型要尽可能的快，不要担心质量，用一个页面满足需求，不要担心设计和代码质量，使用任何可以利用的工具，任何语言，不要在乎语言的特性

* 思考
**有时候是不是都可以不用编程实现？**

### principle 14:grow systems incrementally
* 增量式的开发系统
一个有效的减少软件开发风险的方法时逐步递增的开发软件，从一个只实现了几个小功能的系统开始，然后逐步扩大涵盖越来越多的功能。优势是1.每次构建风险低；2.看到一个版本的产品后，容易帮助客户发现他们还需要什么功能；劣势是如果已开始选择了不合适的架构，那么后续就需要重新设计，以实现新的功能。通过开发抛弃型的原型来避免这个风险。

* 思考
**脚手架的作用，最小的起步集合。对架构设计的要求比较高。现在的做法似乎是微服务，把大的系统拆成小的服务，每一个自己互相独立，单独部署，互不影响。这样先开发核心的服务，然后再开发非核心的，由于进行了一次拆分，每一个服务的功能复杂度下降，也降低了设计的复杂性**

### principle 15:the more seen, the more need

* 看到越多需要的就越多
已经被证明，给用户提供越多的功能/性能，用户就会需要更多的功能/性能。你必须要对此做好准备，无论是经理还是工程师，一旦客户看到了一个产品，他们就会需要更多。这也意味着，每个开发文档都行开被保存和管理好，以备将来。意味着配置管理也应该在发布很久前就完善，要准备好应付客户的口头和书面的请求，也意味着设计要选择的够好，足够支持功能的变化，和性能的提升需要。

* 思考
**对于互联网产品，用户不是一个特定的人，每个人需要的不一样，他们看到第一个版本的产品后，也会有很多新的想要的功能，我们必然不能全部接受，要有权衡的去实现。虽说设计时要考虑到性能，和功能的后续变动，但是亦不可过度设计。这其中的折衷点在于，如果后续的变化能带来的收益足够支持重新开发新的系统，那么一开始的系统能满足达到这个收益前的需求即可**

### principle 16:change during development is inevitable
* 开发过程中的变化是不可避免的
无论你在软件开发的那个阶段，系统的变化都是不可避免的，这种变化会持续整个阶段。软件系统的变化和软件不是后导致需求的变化并不一样。这种变化体现在新的代码，新的计划，新的测试，还有修复产品中新发现的错误，或者提升现有产品的性能。为了让自己能够准备应付这些变化，要保证软件开发中的各个产品是交叉引用的？每次更新的管理要到位。预算和开发的排期要留上buffer，以防哪些关键的更新没有资源开发

* 思考
**需要花费的时间总比我们预计的要多**

### principle 17:if possible, buy instead of build
* 如果有可能，购买而不是自己构建
唯一一个最有效减少软件开发花费日益扩大的方法就是买一个软件，而非从最原始的开始开发。购买的软件只能满足75%的需求，但是可能要花十倍的价钱才能开发一个100%满足需求的软件，而且还要承担超过预算，逾期的风险。而等它开发完后可能会发现，其依旧只满足了75%的需求。作为一个消费者，新的软件开发项目一开始看起来总是令人兴奋的，团队会乐观于完美的方案。只有很少软件开发的过程是顺利的，逐步升高的预算会导致部分功能会砍掉，最后和在售的软件系统提供的功能差不多。作为一个开发者，你需要尽可能的重用软件，重用就是购买而不是自己构建。

* 思考
**大多数时候自己开发的成本可能更高，比如检索系统自己开发而不用ES，虽然我们会找一堆理由，一堆新功能，但是最后花了很大的代价，而且公司内部往往KPI考虑，从零开始开发的KPI收益会大于复用之前的。另一方面，现成的软件，尤其是开源的，可能通用性很高，但是对于公司自己的业务，可能并不完全match，导致部分的性能浪费，部分功能无法实现。如果，性能是项目的关键，这个缺失的主要功能是项目的关键，那么我认为还是有必要开发新的系统**

### principle 18:build software so that it needs a short users's Manual
* 开发的软件要有一个尽量短小的用户手册
一个衡量软件质量的方法就是查看其用户手册的大小。手册越短，软件质量越好。一个好的设计的软件应该是自说明的。不幸的是，太多的软件设计者把自己说成了一个人机交互界面设计的专家，但是大量的手册证明，他们并不如他们声称的那么优秀。使用标准的接口/接口。使用工业级的专家去设计自说明的图标，命令，协议和用户界面。并且记住，只是因为软件开发者喜欢这个接口/界面，并不意味着你的客户会知道如何使用它。许多软件开发者用一些tricks的技术构建了简短，省略的接口。通常，客户喜欢的是简单，清晰的接口，并不是trick的。

* 思考
**这一点，作为普通的2C产品，或许大多数开发人员还能考虑的周到，但是作为2B的软件，或者作为公司内部的软件，往往设计的就每那么好。商业软件，里面功能众多，及其复杂，作为开发人员可能尚不了解全部功能的使用，更不要提普通小客户了。但是由于商业系统可能以帮助客户赚钱/省钱为目的，这方面的容忍度一般B端软件比C端软件的客户要大。另一方面，公司内部开发的系统和平台，开发者往往觉得自己会用，就认为别人也会用，即使大家都是开发人员，但是不具备你的背景，那么也不一定了解你的产品怎么用，从而导致后续有复杂的，疏于维护的wiki，增加了许多使用上的沟通问题，并且导致了反复造轮子，反复开发原有功能。**

### principle 19: every complex problem has a Solution
* 每一个复杂的问题都会有一个解决方案
有人说，“每一个复杂的问题都会有一个 **简单的** 解决方案，这是错的”，要高度怀疑，如果任何人告诉你，“跟随以下10个简单的步骤，你的软件质量问题就会解决”
* 思考
**复杂问题会有一个解决方案，但是这个方案可能不一定简单。同时自己有一个经验，可以补充一下，80%复杂的问题（尤其指bug），其实都是由一些简单的小问题造成的，比如少些一个字母，大小写错误，编码错误，误删除了一行代码等等。因为这种错误不在我们的预期之内，所以程序后续的错误会让我们觉得很复杂，无从下手，不必太过慌张，仔细检查，能解决大多数的问题。**

### principle 20:record your assumption
* 记录下你的假设
我们部署软件的软件可能是各种各样的，并且不可能全部明晰。当我们构建软件，在这样的一个环境中去解决问题时，我们就会对这个环境有许多假设。有人说每10行，每20-30行代码就会有一个假设。有限的假设和无限可能的真是世界，就会产生问题。比如有些假设，最后就会被验证是错误的。需求分析，设计，编码，测试时，不可能会注意所有的假设。所以，建议用一个本子记录下所有的假设。即使这些假设看起来显而易见，或者如果不这么假设是显然违反常理的。同时也要记录下假设的实现，这样就能和项目中的该假设对比，看其是否体现了出来。理想情况下，每一个假设都会有一个实现进行封装隔离。

* 思考
**有假设就要考虑假设的可行性，不能太理想化，有一些错误必须要考虑。假设要尽可能的正确，所有有些关键的假设要找数据，方法去论证其正确性。比如一个流量预估系统，我们会有一个假设，每天的流量是差不多的，每个词上的流量也是差不多的，这样才能预估。但是这个假设本身对不对呢？作者把假设进行封装的思想很有意思，减少假设之间的耦合性，这样一旦现实环境的某一项变化了，针对其的假设就可以轻易的变化。**

### principle 21:different languages for different phases
* 不同的阶段用不同的语言
工业界的终极渴望是用简短的方案解决复杂的问题，这驱动了许多声称最好的软件开发方法，可以用同一套符号来描述软件开发的整个生命阶段。既然这种方案不存在于其他的工程科学中，那为什么会存在在软件工程中呢？电器工程师用不同的符号语言，在不同的设计活动中。符号提供给了我们模型去描述我们脑中的思想，越多的符号就会越丰富我们表达的方式，从而我们就能更好的理解，具体化我们的产品。为什么软件工程师在需求分析，设计，编码阶段用同样的语言？为什么要把面向对象用在程序开发的所有阶段呢？在不同的阶段之间转化是很困难的，用相同的语言也无济于事。当然，如果一个语音真的那么理想适合多个阶段，那就果断用它。

* 思考
**不能迷信面向对象编程，和函数式，过程时都要用，那个合适用哪个，现在语言中的lambda表达式就是函数式编程的东西。如果一个方法和类中的对象并没有什么关系，那么完全可以独立出一个函数，对于明显过程化的业务， 比如报表之类的，就很时候面向过程开发**

### principle 22:Technique before tools
* 技术在工具之前
一个没用经过训练的木匠，给他厉害的工具，他会编程一个危险的新手木匠。一个没经过训练的软件工程师也是同样。当你使用一个工具时，你需要被充分训练过，了解工具，并且遵守软件开发的技术。当然也需要知道如何使用工具，当然这相对于好的训练来说是第二位的。强烈建议手工的的实现一个技术，并且向你自己和经理证明这个技术是可以工作的，在引入自动化的工具之前。大多数情况下，如果一个技术在非自动化时无法工作，那么自动化了也不能用。

* 思考
**使用一个工具时要了解其原理，知其然也要知其所以然，比如用valgrind去分析C++程序，要了解其原理，知道这个原理是可行的才可以开发这样的工具。先用原始的方法验证技术，然后再自动化，自动化是为了效率的提升，但使用技术解决问题才是真正的价值。**

### principle 23:use tools, but be realistic
* 使用工具，但是要注意现实
软件工具会帮助它的使用者提升效率，无论如何请使用他们。就像一个文字编辑器是作家有效的帮手，一个CASE工具对于软件开发者也是大的助力。提升初始化工作10-20%效率，提升修改效率25-50%。但是软件开发最重要的工作，思考，是无法通过工具完成的。要真实的评价CASE工具的使用对生产力的提升，大约70%的CASE工具被购买后没有使用。我觉得首要原因是对工具过分乐观了，然后结果是令人失望的，而非工具本身没有效果。
>CASE tools 为Computer-Aided Software Engineering tools的缩写，意义为“计算机辅助软件工程工具"。 目标是通过一组工具和方法使软件系统成为一种高质量，规范化，方便维护的软件产品。 它也涉及到信息系统发展中所使用的方法和自动化领域中软件开发相关内容。

* 思考
**软件开发的10%的工作才是编码，对于个人来说思考花的时间多，对于整个团队来说用在沟通协作上的时间更多。工具并不能大幅度的提升效率，尤其是对思考而言，从而也不要迷信有什么工具的引入会大幅缩短开发时间。对于沟通来说，好的软件倒是的确能提高效率，但考虑到沟通的本身也是思考的一种体现，所以其能做到的也是有限**

### principle 24:give software tools to good engineers
* 给好的工程师工具
文字编辑器能提升作家的效率，但是不能把一个糟糕的小说变好，工具也不能把一个糟糕的软件工程师变成优秀的。只给好的工程师工具，因为给了差的工程师工具，反而会提升他们生产低质量代码的效率。

* 思考
**质量本身无法通过工具提升，不过工具现在倒是可以提供检测，告诉你代码的质量，从而让你修改，从这一方面看，这种工具相当于提升了工程师的基础素质，也激励了优秀者想要优秀，需要更加的努力。**

### principle 25:CASE tools are expensive
* CASE工具的价格是昂贵的
主要考过购买价格，软件使用的培训费用，后期每年的许可费用，CASE是有用的，也是要做必要的投资的，要分析预算和回报时考虑到CASE工具的高额花费，但也要考虑到，不买这个工具可能会带来的更好的费用，比如低的生产率，质量，延期交付等成本。

* 思考
**一个工具的是否使用，一件东西的买与不买，不能只看价格的贵与便宜，要看投入产出比，哪一种性价比更高就选择那一个，不要拘泥于定式。我们会觉得日常看法中，软件工程的项目管理相关软件的使用非常麻烦，各种卡片，流程要走，看似是一个不小的代价。但如果没有这些可能导致的代价会更大。这个地方的难点就在于，不是所有的东西都那么容易衡量价值，代价。**

### principle 26:know-when is as important as know-How
* 知道何时做和知道如何做同样重要
在软件开发中，经常有一个工程师学到了一项新技术，并把它当作解决其他一切技术的替代。于此同时组里另一个工程师也是如此，于是不可避免的成轮就发生了。事实上两者都不对。知道如何使用一个新技术，不能使这个技术变成一个好的技术，同时也不能使你自己成为一个优秀的工程师。就像会使用木工车床不能让你成为一个优秀的木匠。优秀的工程师知道数十种不同的技术，并且知道在一个项目中何时该使用其中那一个。当做需求分析时，要知道那种技术最适合解决当前的问题。做设计时要只能那种技术最能描述系统，做编码时选择最合适的编程语言。

* 思考
**对于初学者来说，不必纠结于该学JAVA还是C++，这俩你都需要会，还需要会Python，Go，Shell等等。同时也要明白一个新技术出现的背景，和他适用的问题，不要人云亦云，看Go出来了，就什么项目就像用Go。不要会了多线程技术，就什么都要多线程，同时，线程池，缓存，生产者消费者模型，protobuf等都是这样。比如最近我的一个项目，为了提升效率，直接把二进制进行持久化，而不用protobuf。**

### principle 27:stop when you achieve your goal
* 达到目标时就请停止
软件工程师会用多种方法和技术，它们每一个都是为了一个目的出现的，同时又是为了解决项目中的一个子问题。比如面向对象分析的目标是了解要解决的问题。比如DARTS的目标是架构设计等。每一个情况下，这个技术会包含一系列的步骤，不要为了应用这个技术而忘了问题本身。不要对目标的变化有负罪感。如果你发现这个技术应用了一半，问题就解决了，那么及时停止。另一方面，也要有软件开发的全局视野，要明白这个技术后续的步骤的增加，可能会导致其他的风险，从而产生新的问题。

* 目标
**这点感觉在互联网的开发中，大家重视效率，一般都是开发到能用就上线了，有时候可能有些必要的步骤都还没做，这种做了过多的步骤的情况似乎并不多见。可以从其他方面理解，比如不要为了炫技，目标是解决问题。不要过度设计，过度考虑容错，从而引入了过多复杂的保障性措施，从而使得问题的解决占的比例下降**

### principle 28:know formal methods
* 要知道形式化方法
形式化方法如果没有很强的离散数学功底是很难掌握的。从另一个方面说，使用形式化的方法能明确软件开发中许多没有覆盖的问题。每个项目中至少要有一个人能够熟悉形式化方法，从而保证构建的软件是有质量的。许多人认为唯一需要使用形式化方法的地方是用他们来详细说明一个系统的完成度。这个理解并不对，事实上，最高效的方法是写一个口语的说明书。然后试着用形式化的方法写其中的部分。试着用形式化的方法来书写会帮助你发现口语中的问题。进一步修改口语中的问题，就能等到一个好的说明书。在形式化主义帮助你后就请忘了它。

* 思考
**形式化有严格的规则，能帮助明确问题，提高系统的可靠性和健壮性，成本高**

### principle 29:align reputation with organization
* 把名声和组织结合在一起
日本软件工程师看待软件bug的佳都不同于美国工程师。其中一个差异是，在日本一个产品的错误会让公司丢脸，公司的丢脸又会导致软件工程师愧作为一个工程师。这产生的原因是相对于美国，日本工人一般会在一家企业工作一辈子。通常，当任何人发现一个软件中的错误时，工程师应该是感恩的，而不是又挫败感。会产生错误才是人类。接受它，克服它。发现错误应该把它告诉其他人，而不是隐藏它。把错误告诉其他人可以避免其他人犯同样的错误。也可以为了未来没防范的错误被修复做好准备。

* 思考
**和公司的KPI设定有关，一个错误的发生不能让一个人完全背锅。应该合力去解决。Case Study也是必要的，不是为了批斗，检讨而是为了从中学习，这个问题涉及到人性，很难处理，一定要从文化上去引导。如果一切符合规则，流程，犯了错误就不能只指责某个人。Case study时，其他的人也应该说下，如果自己遇到这样的问题该怎么办，而不是只有犯错的人反思。**

### principle 30:follow the lemming with care
* 小心从众
5000千万人认同一件愚蠢的事情，它依旧是愚蠢的。比如面向对象，软件管理，软件重用，CASE工具，原型开发。这些东西都是这样，适用的公司用了才会又效果，要考虑自身的情况。当学习一个新技术时，不要很快的就全盘接受。仔细了解，小心其中的风险和代价。做必要的试验。

* 思考
**乌合之众。不要盲目的随大流，要有自己的思考，如果自己思考后认为的确是这样，那么跟随大众就没问题。也不是为了特立独行而特立独行，关键是要有思考。对于软件开发，还是要了解每个技术，方法的存在背景，适用场景，以及它的trade off。**

### principle 31:don't ignore technoloy
* 不要忽略技术
软件开发技术日新月异，你不可能长期保持不变，如果缺少对新技术的学习。技术的发展往往是一个一个的浪潮，通常一个浪潮5-7年，新的浪潮在之前最高效的技术上面又进一步的发展。两个保持自己对新技术的渴求的方法就是，1读正确的杂志，2和正确的人交谈。不要只和自己公司的人交谈，每年参加一两次会议。会议中的演讲可能不如你在大厅里与人的交谈。

* 思考
**持续学习，不要不了解一个东西就去嘲笑它，比如最近的区块链，有些人看不起这个技术，认为都是骗钱的，应该先去充分了解学习。不能只依靠网络上的博客文章的知识，要寻找可以交流的人，思想要进行碰撞，交流才能互相精进。以后参加会议，要多搭讪认识不同的人，不能只傻傻听**

### principle 32:use documenttation standards
* 使用文档化的标准
组织和项目中又标准就要遵守，永远不要把做了一件错误的事情，怪罪到标准上。遵循标准的基础上也要革新，要有智慧的遵守，即使你没有被要求遵守某项准则，也可以拿一个准则作为checklist。

* 思考
**要灵活的变通，不能过于死板。比如代码规范，也有可以豁免的情况。上线的功能，如果没有影响可以先带上去等等。原则性的规范不要违反，其他的灵活调整。作为管理者也要了解这点，不能苛求员工。**

### principle 33:every document needs a glossary
* 文档都要有一个词汇表
文档中要有一个词汇表，以免读到不明白其含义的词的时候有地方可以查。一个做法是，在一个专业名词出现时在下方有常见的话进行解释，然后再用专业的定义进行解释。

* 思考
**体现出一个思想，你写的文档，代码，等是给别人看到的，要站在别人的角度上思考问题，别人可能是初学者，也可能是专业人士。**

### principle 34:every software document needs an index
* 每个软件的文档都需要一个索引
文档中有一个列表，标注了每个词和概念出现的位置和页码。在需求分析，设计，编码，测试，用户手册中的文档都需要。尤其是在后期软件的维护和升级中。现在的文字编辑器有这些自动化的功能来生成索引。

* 思考
**反观公司的商业化的软件，使用复杂不说，配套的用户文档也十分不健全，使用困难。现在很多地方采用了视频化的文档，但是这种效率较低。其他阶段的文档就更不健全了，而且关键的是更新不及时。很大的原因时，互联网的软件开发生命周期都太短了，一个产品一共也就一辆年，不像传统软件一开发就是一两年。**

### principle 35:use the same name for the same concept
* 相同的概念用相同的名字
和小说不一样，技术文档要用相同的词表达相同的概念，相同的句式表达相似的信息。

* 思考
**日常的开发中，有时候同一个项目都有不同的名词，有时候用项目代号，有时候产品名称，有时候又用简称。增加交流成本。写技术文档时，要明确不要各种修饰，词藻。**

### principle 36:research-then-transfer donesn't work
* 研究然后转化为现实的道路并不好用
有不少软件工程技术被研究出来，但是很少使用。1.通常软件研究者的实际开发部署经验少。2.研究人员发现的某种简单技术解决问题的方法，并没有经过大量时间的验证，这个方法是否真的适合现实环境。3.研究人员和实际开发人员有很多分歧，互相难以交流。把研究结果转化为工业中切实可用的方案，一个方法就是增强两者之间的联系，用真实的环境。

* 思考
**这可能是这个上个时代容易出的问题，现在学校科研机构和工业界的结合比以前要好多了。不过也提示我们切记闭门造成，要及早的到现实世界中去验证**

### principle 37:take responsiblilty
* 负责任
在所有的工程原则中，当一个设计失败，工程师会被责备。比如在桥梁坍塌后，我们会问工程师做错了什么。但是当软件失败时，却很少责备工程师。软件工程师有很多借口逃避责任，所以就会导致糟糕的设计。There are no excuses。如果你是系统的开发容易，你的责任是保证系统正确。负责任，要么就不要做。

* 思考
**责任心，的第一步是完成交代的工作，对齐质量，结果负责。第二步就是要有Owner精神，对整个项目负责。原则性的错误不能去反，无法避免的错误要用丰富的知识和经验，尽量去避免。**

## chapter 3:Requirement engineering principles 需求分析准则
需求阶段两个过程，1，学习这个需要一个解决方案的问题。2.封装一个黑盒系统来解决问题

### principle 38:poor requirement yield poor cost estimates
* 差的需求分析，导致差的预算估计
利用原型开发减少不正确的需求的风险，利用配置管理来控制变化。计划好未来发布后会有新的需求。用更加正规的方法去做需求分析。

* 思考
**会有项目开发一半了，发现要推到重来。PM和RD要沟通好，RD要明确PM的需求，可以通过复述的方式。同时PM也要真的理解客户的需求，这一步可能更难一些，不能过分依赖调研，调研的结果有时候有导向性，有时候客户会潜意识的欺骗。**

### principle 39:determine the problem before wrting requirements
* 在写需求之前先要决定问题是什么
不能一面对问题，就不去思考，立马开始提供方案，要进行分析。一个大楼里，租户觉得等电梯的时间长了浪费时间，作为大楼里的管理者，觉得是租户多了，而不是电梯少了。于是方案应该是增加电梯的速度，而不是增加新电梯，提高租金，甚至修改电梯算法等方法。遇到问题时要尽可能的考虑都有谁，遇到了什么问题。当解决问题时，不要被第一个令人激动的方案所迷惑。流程上的一些改变会比构建一个系统便宜的多。

* 思考
**一个问题中会有参与的多方，要从不同方的角度思考问题。就像广告系统，不能只考虑到商家，也要考虑到消费者，这样就会明白，消费者不愿意看到不感兴趣的恶趣味广告，于此同时消费者也确有购买商品或者服务的需求。**

### principle 40:determine the requirements now
* 现在就决定需求
需求是很难理解和明确的。一个错误的做法就是潦草的明确需求说明文档，然后就冲过去开始设计和编码。这种错误的方法的假设是：1.任何系统都好过没有系统。2.需求迟早会明确。3.设计人员会在构建系统的时候指出什么能够构建开发。正确的方法是，当前要尽可能的了解和学习需求。做原型，和客户交谈，收集数据。然后再文档化需求。逐步迭代增量的开发，但是每次增量的开发都不能没有好的需求分析。

* 思考
**人们总是相信行动比不行动好，有时候并不这样，要观察和思考。这里要有作者提到的一些分析的方法，也不能干想而不动手，长期没有可见的进展容易导致人心涣散，缺乏干劲，要把明确需求深入到骨髓中去。**

### principle 41:fix requirements specification errors NOW
* 现在就修复需求说明中的错误
需求说明中的错误，会导致后期的工作用几十，上百倍的代价修复它。

* 思考
**一定要尽早的发现问题，如果是不确定的问题，觉得有风险的要及时抛出，给合作同学，上下游知道。**

### principle 42:prototypes reduce risk in selecting user interfaces
* 原型可以减少选择用户界面的风险
开发界面非常简单，不但能明确需求，好的界面也会赢得客户的信心。

* 思考
**互联网中一般不好直接给用户提供只有一个界面的原型，多少还是要有一些功能。不过设计人员开发早期的界面原因，能让整个团队对产品有更直观的感觉，便于明确问题。一图胜千言。这也是为何UE重要，现在PM一般要有这种界面设计的能力，便于提需求。**

### principle 43:record why requirements where included
* 记录下在何地，为何引入了这个需求
记录下需求引入的时间和背景，这样后续有变更的时候可以溯源

* 思考
**现在大多交流以IM工具进行，加上邮件，天然有记录，但是为了管理方便，对于会议要有会议总结，需求的修改要及时更新到MRD文档中，并让相关同学及时知晓。**

### principle 44:Identity subsets
* 定义子问题
定义需求的最小集合。每次增量开发的最小集。记录下每个版本包含的功能集合。甚至要记录不同的客户，不同的版本有哪些功能。

* 思考
**就是功能分优先级的思想，对于2B的商业软件，会有不同客户的不同定制化功能，也要进行分类和管理。对于开发人员来说，要写明白每个代码CI的注释，便于分辨哪些关键功能是哪些版本加入的。**

### principle 45:review the requirements
* 检查需求
自然语言写的需求不利于后续的检查，应该用更规范正式的语言来写需求。

* 思考
**把聊天确定的需求文字化，把文字化的东西正规化。**

### principle 46:avoid design in requirements
* 避免在需求分许时提前开始系统设计


### principle 60:
### principle 86:
