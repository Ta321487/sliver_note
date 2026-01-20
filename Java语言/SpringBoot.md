# SpringBoot

## 1.回顾

### 1.1回顾学习路线

1. javase：OOP
2. mysql：持久化

3. html+css+Jquery+框架：视图

4. javaweb：独立开发mvc三层架构的网站：原始

5. SSM：框架：简化了开发流程：配置也开始较为复杂；
   war：tomcat 运行
6. Spring再简化：Spring Boot；jar ：内嵌tomcat；微服务架构！

7. 服务越来越多：Spring Cloud 整理服务



### 1.2鸡汤

培训讲师
  （面向面试培训，叫你如何使用，快速上手！）

做教育的
  如何学习新东西，如何持续学习，如果关注这个行业！
  知道这个东西的来龙去脉，历史，理论；（用来做什么？怎么用？）

程序 = **数据结构+算法（集合框架）**；（程序猿）

程序 = **面向对象+框架**；（码农）



### 1.3回顾Spring

**什么是Spring ？**

**Spring 是一个开源框架，2003年兴起的一个轻量级java 开发框架**，Rod Johnson（音乐学的博士，本科不是计算机，头发挺多的）
Spring 是为了解决企业级应用开发的复杂性而创建，简化开发



**Spring是如何简化开发的？**

1. 基于POJO的轻量级和最小侵入性编程，**所有的东西都是bean**
2. 通过**IOC、和依赖注入（DI）和面向接口实现松耦合**
3. 基于**切面（AOP）和惯例进行声明式编程**
4. **通过切面和模板减少样式代码**，RedisTemplate



## 2.SpringBoot阶段开发

### 2.1什么是SpringBoot

  过javawed的就知道，开发一个web应用，**从最初开始接触Servlet结合tomcat 。跑出一个hello world程序**，是要经历特别多的步骤；后面就用来Spring MVC框架，到现在的Spring Boot，过一两年可能又会有其他框架出现；有经历过框架的不断演进，然后自己开发项目所有的技术也在不断的变化、改造吗？

**什么是Spring Boot呢？就是一个javawevb的开发框架**，和SpringMVC类似，对比其他javaweb框架的好处，官方说是“简化开发”，约定大于配置，能迅速的开发web应用，几行代码开发一个http接口。
所有的技术框架的发展似乎都遵循了一条主线规律：从一个复杂应用场景 衍生 一种规范框架，人们只需要进行各种配置而不需要自己去实现它，这时候强大的配置功能成了优点；发展到一定程度之后，人们根据实际生产应用情况，选取其中实用功能和设计精华，重构出一些轻量级的框架；之后为了提高开发效率，嫌弃原先的各类配置过于麻烦，于是开始提倡“约定大于配置”，进而衍生出一些一站式的解决方案。

是的这就是Java企业级应用->J2EE->spring->springboot的过程。



随着 Spring 不断的发展，涉及的领域越来越多，项目整合开发需要配合各种各样的文件，慢慢变得不那么易用简单，违背了最初的理念，甚至人称配置地狱。Spring Boot 正是在这样的一个背景下被抽象出来的开发框架，目的为了让大家更容易的使用 Spring 、更容易的集成各种常用的中间件、开源软件；



**Spring Boot 基于 Spring 开发**，Spirng Boot 本身并不提供 Spring 框架的核心特性以及扩展功能，只是用于快速、敏捷地开发新一代基于 Spring 框架的应用程序。也就是说，它并不是用来替代 Spring 的解决方案，而是和 Spring 框架紧密结合用于提升 Spring 开发者体验的工具。Spring Boot 以约定大于配置的核心思想，默认帮我们进行了很多设置，多数 Spring Boot 应用只需要很少的 Spring 配置。同时它集成了大量常用的第三方库配置（例如 Redis、MongoDB、Jpa、RabbitMQ、Quartz 等等），Spring Boot 应用中这些第三方库几乎可以零配置的开箱即用。
简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，spring boot整合了所有的框架 。



**Spring Boot 出生名门（Spring已经很火了）**，从一开始就站在一个比较高的起点，又经过这几年的发展，生态足够完善，Spring Boot 已经当之无愧成为 Java 领域最热门的技术。



**Spring Boot的主要优点：**
  1.为所有Spring开发者更快的入门
  2.开箱即用，提供各种默认配置来简化项目配置
  3.内嵌式容器简化Web项目
  4.没有冗余代码生成和XML配置的要求



### 2.2.SpringBoot 阶段

SpringBoot 简化Spring的 ，和Spring本质上是一样的。

1. 是什么
2. 配置如何编写 yml
3. 自动装配原理（最核心）
4. 集成web开发（拦截器，登录认证，增删改查）
5. 集成数据库（druid）
6. 分布式开发：Dubbo+zookeeper（必须掌握）
7. swagger：接口文档
8. 任务调度
9. SpringSecurity ： Shiro（安全框架），全程横切进去（AOP）



## 3.微服务

### 3.1什么是微服务

“微服务架构（Microservice Architecture）”一词在过去几年里广泛的传播，它用于描述一种设计应用程序的特别方式，作为一套独立可部署的服务。目前，这种架构方式还没有准确的定义，但是在围绕业务能力的组织、自动部署（automated deployment）、端智能（intelligence in the endpoints）、语言和数据的分散控制，却有着某种共同的特征。
“微服务（Microservices）”——只不过在满大街充斥的软件架构中的一新名词而已。尽管我们非常鄙视  这样的东西，但是这玩意所描述的软件风格，越来越引起我们的注意。在过去几年里，我们发现越来越多的项目开始使用这种风格，以至于我们身边的同事在构建企业级应用时，把它理所当然的认为这是一种默认开发形式。然而，很不幸，微服务风格是什么，应该怎么开发，关于这样的理论描述却很难找到。
  简而言之，微服务架构风格，就像是把一个单独的应用程序开发为一套小服务，每个小服务运行在自己的进程中，并使用轻量级机制通信，通常是 HTTP API。这些服务围绕业务能力来构建，并通过完全自动化部署机制来独立部署。这些服务使用不同的编程语言书写，以及不同数据存储技术，并保持最低限度的集中式管理。
  在开始介绍微服务风格（microservice style）前，比较一下整体风格（monolithic style）是很有帮助的：一个完整应用程序（monolithic application）构建成一个单独的单元。企业级应用通常被构建成三个主要部分：客户端用户界面（由运行在客户机器上的浏览器的 HTML 页面、Javascript 组成）、数据库（由许多的表构成一个通用的、相互关联的数据管理系统）、服务端应用。服务端应用处理 HTTP 请求，执行领域逻辑（domain logic），检索并更新数据库中的数据，使用适当的 HTML 视图发送给浏览器。服务端应用是完整的 ，是一个单独的的逻辑执行。任何对系统的改变都涉及到重新构建和部署一个新版本的服务端应用程序。
  这样的整体服务（monolithic server）是一种构建系统很自然的方式。虽然你可以利用开发语基础特性把应用程序划分成类、函数、命名空间，但所有你处理请求的逻辑都运行在一个单独的进程中。在某些场景中，开发者可以在的笔计本上开发、测试应用，然后利用部署通道来保证经过正常测试的变更，发布到产品中。你也可以使用横向扩展，通过负载均衡将多个应用部署到多台服务器上。
整体应用程序（Monolithic applications）相当成功，但是越来越多的人感觉到有点不妥，特别是在云中部署时。变更发布周期被绑定了——只是变更应用程序的一小部分，却要求整个重新构建和部署。随着时间的推移，很难再保持一个好的模块化结构，使得一个模块的变更很难不影响到其它模块。扩展就需要整个应用程序的扩展，而不能进行部分扩展。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2d0057f14696404c88ed8141cb93e0c3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





**微服务风格的特性**

  这导致了微服务架构风格（microservice architectural style）的出现：把应用程序构建为一套服务。事实是，服务可以独立部署和扩展，每个服务提供了一个坚实的模块边界，甚至不同的服务可以用不同的编程语言编写。它们可以被不同的团队管理。
  我们必须说，微服务风格不是什么新东西，它至少可以追溯到 Unix 的设计原则。但是并没有太多人考虑微服务架构，如果他们用了，那么很多软件都会更好。



**组件化（Componentization ）与服务（Services）**

自从我们开始软件行业以来，一直希望由组件构建系统，就像我们在物理世界所看到的一样。在过去的几十年里，我们已经看到了公共库的大量简编取得了相当的进步，这些库是大部分语言平台的一部分。
  当我们谈论组件时，可能会陷入一个困境——什么是组件。我们的定义是，组件（component）是一个可独立替换和升级的软件单元。
  微服务架构（Microservice architectures）会使用库（libraries），但组件化软件的主要方式是把它拆分成服务。我们把库（libraries）定义为组件，这些组件被链接到程序，并通过内存中函数调用（in-memory function calls）来调用，而服务（services ）是进程外组件（out-of-process components），他们利用某个机制通信，比如 WebService 请求，或远程过程调用（remote procedure call）。组件和服务在很多面向对象编程中是不同的概念。
  把服务当成组件（而不是组件库）的一个主要原因是，服务可以独立部署。如果你的应用程序是由一个单独进程中的很多库组成，那么对任何一个组件的改变都将导致必须重新部署整个应用程序。但是如果你把应用程序拆分成很多服务，那你只需要重新部署那个改变的服务。当然，这也不是绝对的，有些服务会改变导致协调的服务接口，但是一个好的微服务架构的目标就是通过在服务契约（service contracts）中解耦服务的边界和进化机制来避免这些。
  另一个考虑是，把服务当组件将拥有更清晰的组件接口。大多数开发语言都没有一个良好的机制来定义一个发布的接口（Published Interface）。发布的接口是指一个类向外公开的成员，比如 Java 中的声明为 Public 的成员，C# 中声明为非 Internal 的成员。通常只有在文档和规范中会说明，这是为了让避免客户端破坏组件的封装性，阻止组件间紧耦合。服务通过使用公开远程调用机制可以很容易避免这些。
像这样使用服务也有不足之处。远程调用比进制内调用更消耗资源，因此远程 API 需要粗粒度（coarser-grained），但这会比较难使用。如果你需要调整组件间的职责分配，当跨越进程边界时，这样做将会很难。
一个可能是，我们看到，服务可以映射到运行时进程（runtime processes）上，但也只是一个可能。服务可以由多个进程组成，它们会同时开发和部署，例如一个应用程序进程和一个只能由这个服务使用的数据库。



**围绕业务功能的组织**

当寻找把一个大的应用程序拆分成小的部分时，通常管理都会集中在技术层面，UI团队、服务端业务逻辑团队和数据库团队。当使用这种标准对团队进行划分时，甚至小小的更变都将导致跨团队项目协作，从而消耗时间和预算审批。一个高效的团队会针对这种情况进行改善，两权相害取其轻。业务逻辑无处不在。实践中，这就是 Conway’s Law 的一个例子。
  设计一个系统的任何组织（广义上）都会产生这样一种设计，其结构是组织交流结构的复制。
——Melvyn Conway, 1967
  Melvyn Conway 的意识是，像下图所展示的，设计一个系统时，将人员划分为 UI 团队，中间件团队，DBA 团队，那么相应地，软件系统也就会自然地被划分为 UI 界面，中间件系统，数据库。
![在这里插入图片描述](https://img-blog.csdnimg.cn/7e4160f4fd7947e08f2532eff9beba15.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



微服务（microservice ）的划分方法不同，它倾向围绕业务功能的组织来分割服务。这些服务实现商业领域的软件，包括用户界面，持久化存储，任何的外部协作。因此，团队是跨职能的（cross-functional），包含开发过程所要求的所有技能：用户体验（user-experience）、数据库（database）和项目管理（project management）
![在这里插入图片描述](https://img-blog.csdnimg.cn/49248cfe65934f3ebe812c7344fc34c2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



www.comparethemarket.com就是采用这种组织形式。跨职能的团队同时负责构建和运营每个产品，每个产品被分割成许多单个的服务，这些服务通过消息总线（Message Bus）通信。

  大型的整体应用程序（monolithic applications）也可以按照业务功能进行模块化（modularized），尽管这样情况不常见。当然，我们可以敦促一个构建整体应用程序（monolithic application ）的大型团队，按业务线来分割自己。我们已经看到的主要问题是，这种组件形式会导致很多的依赖。如果整体应用程序（monolithic applications）跨越很多模块边界（modular boundaries ），那么对于团队的每个成员短期内修复它们是很困难的。此外，我们发现，模块化需要大量的强制规范。服务组件所要求的必需的更明确的分离使得保持团队边界清晰更加容易。



**产品不是项目**

大部分的软件开发者都使用这样的项目模式：至力于提供一些被认为是完整的软件。交付一个他们认为完成的软件。软件移交给运维组织，然后，解散构建软件的团队。
  微服务（Microservice ）的支持者认为这种做法是不可取的，并提议团队应该负责产品的整个生命周期。Amazon 理念是“你构建，你运维（you build, you run it）”，要求开发团队对软件产品的整个生命周期负责。这要求开发者每天都关注他们的软件运行如何，增加更用户的联系，同时承担一些售后支持。
  产品的理念，跟业务能力联系起来。不是着眼于完成一套功能的软件，而是有一个持续的关系，是如何能够帮助软件及其用户提升业务能力。
  为什么相同的方法不能用在整体应用程序（monolithic applications），但更小的服务粒度能够使创建服务的开发者与使用者之间的个人联系更容易。



**强化终端及弱化通道**

当构建不同的进程间通信机制的时候，我们发现有许多的产品和方法能够把更加有效方法强加入的通信机制中。比如企业服务总线（ESB），这样的产品提供更有效的方式改进通信过程中的路由、编码、传输、以及业务处理规则。

  微服务倾向于做如下的选择：强化终端及弱化通道。微服务的应用致力松耦合和高内聚：采用单独的业务逻辑，表现的更像经典Unix意义上的过滤器一样，接受请求、处理业务逻辑、返回响应。它们更喜欢简单的REST风格，而不是复杂的协议，如WS或者BPEL或者集中式框架。
有两种协议最经常被使用到：包含资源API的HTTP的请求-响应和轻量级消息通信协议。最为重要的建议为：
善于利用网络，而不是限制（Be of the web, not behind the web）。
——Ian Robinson
  微服务团队采用这样的原则和规范：基于互联网（广义上，包含Unix系统）构建系统。这样经常使用的资源几乎不用什么的代价就可以被开发者或者运行商缓存。
  第二种做法是通过轻量级消息总线来发布消息。这种的通信协议非常的单一（单一到只负责消息路由），像RabbitMQ或者ZeroMQ这样的简单的实现甚至像可靠的异步机制都没提供，以至于需要依赖产生或者消费消息的终端或者服务来处理这类问题。

  在整体工风格中，组件在进程内执行，进程间的消息通信通常通过调用方法或者回调函数。从整体式风格到微服务框架最大的问题在于通信方式的变更。从内存内部原始的调用变成远程调用，产生的大量的不可靠通信。因此，你需要把粗粒度的方法成更加细粒度的通信。



**分散治理**

集中治理的一种好处是在单一平台上进行标准化。经验表明这种趋势的好处在缩小，因为并不是所有的问题都相同，而且解决方案并不是万能的。我们更加倾向于采用适当的工具解决适当的问题，整体式的应用在一定程度上比多语言环境更有优势，但也适合所有的情况。

  把整体式框架中的组件，拆分成不同的服务，我们在构建它们时有更多的选择。你想用Node.js去开发报表页面吗？做吧。用C++来构建时时性要求高的组件？很好。你想以在不同类型的数据库中切换，来提高组件的读取性能？我们现在有技术手段来实现它了。

当然，你是可以做更多的选择，但也不意味的你就可以这样做，因为你的系统使用这种方式进行侵害意味着你已经有的决定。
  采用微服务的团队更喜欢不同的标准。他们不会把这些标准写在纸上，而是喜欢这样的思想：开发有用的工具来解决开发者遇到的相似的问题。这些工具通常从实现中成长起来，并进行的广泛范围内分享，当然，它们有时，并不一定，会采用开源模式。现在开源的做法也变得越来越普遍，git或者github成为了它们事实上的版本控制系统。

  Netfix就是这样的一个组织，它是非常好的一个例子。分享有用的、尤其是经过实践的代码库激励着其它的开发着也使用相似的方式来解决相似的问题，当然，也保留着根据需要使用不同的方法的权力。共享库更关注于数据存储、进程内通信以及我们接下来做讨论到的自动化等这些问题上。

  微服务社区中，开销问题特别引人注意。这并不是说，社区不认为服务交互的价值。相反，正是因为发现到它的价值。这使得他们在寻找各种方法来解决它们。如Tolearant Reader和Consumer-Driven Contracts这样的设计模式就经常被微服务使用。这些模式解决了独立服务在交互过程中的消耗问题。使用Consumer-Driven Contracts增加了你的信心，并实现了快速的反馈机制。事实上，我们知道澳大利亚的一个团队致力使用Consumer-Drvien Contracts开发新的服务。他们使用简单的工程，帮助他们定义服务的接口。使得在新服务的代码开始编写之前，这些接口就成为自动化构建的一个部分。构建出来的服务，只需要指出这些接口适用的范围，一个优雅的方法避免了新软件中的’YAGNI '困境。这些技术和工具在使用过程中完善，通过减少服务间的耦合，限制了集中式管理的需求。

  也许分散治理普及于亚马逊“编译它，运维它”的理念。团队为他们开发的软件负全部责任，也包含7*24小时的运行。全责任的方式并不常见，但是我们确实发现越来越多的公司在他们的团队中所推广。Netfix是另外一个接受这种理念的组件。每天凌晨3点被闹钟吵醒，因为你非常的关注写的代码质量。这在传统的集中式治理中这是一样多么不思议的事情呀。



**分散数据管理**

对数据的分散管理有多种不同的表现形式。最为抽象层次，它意味着不同系统中的通用概念是不同的。这带来的觉问题是大型的跨系统整合时，用户使用不同的售后支持将得到不同的促销信息。这种情况叫做并没有给用户显示所有的促销手段。不同的语法确实存在相同的词义或者（更差）相同的词义。
应用之间这个问题很普遍，但应用内部这个问题也存在，特别是当应用拆分成不同的组件时。对待这个问题非常有用的方式为Bounded Context的领域驱动设计。DDD把复杂的领域拆分成不同上下文边界以及它们之间的关系。这样的过程对于整体架构和微服务框架都很有用，但是服务间存在着明显的关系，帮助我们对上下文边界进行区分，同时也像我们在业务功能中谈到的，强行拆分。

  当对概念模式下决心进行分散管理时，微服务也决定着分散数据管理。当整体式的应用使用单一逻辑数据库对数据持久化时，企业通常选择在应用的范围内使用一个数据库，这些决定也受厂商的商业权限模式驱动。微服务让每个服务管理自己的数据库：无论是相同数据库的不同实例，或者是不同的数据库系统。这种方法叫Polyglot Persistence。你可以把这种方法用在整体架构中，但是它更常见于微服务架构中。

![在这里插入图片描述](https://img-blog.csdnimg.cn/e4279bba773a44ad8cc9a032ff9ac411.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



微服务音分散数据现任意味着管理数据更新。处理数据更新的常用方法是使用事务来保证不同的资源修改数据库的一致性。这种方法通常在整体架构中使用。

  使用事务是因为它能够帮助处理一至性问题，但对时间的消耗是严重的，这给跨服务操作带来难题。分布式事务非常难以实施，因此微服务架构强调服务间事务的协调，并清楚的认识一致性只能是最终一致性以及通过补偿运算处理问题。

  选择处理不一致问题对于开发团队来说是新的挑战，但是也是一个常见的业务实践模式。通常业务上允许一定的不一致以满足快速响应的需求，但同时也采用一些恢复的进程来处理这种错误。当业务上处理强一致性消耗比处理错误的消耗少时，这种付出是值的的。



**基础设施自动化**

基础设施自动化技术在过去几年中得到了长足的发展：云计算，特别是AWS的发展，减少了构建、发布、运维微服务的复杂性。

  许多使用微服务架构的产品或者系统，它们的团队拥有丰富的持集部署以及它的前任持续集成的经验。团队使用这种方式构建软件致使更广泛的依赖基础设施自动化技术。下图说明这种构建的流程：


![在这里插入图片描述](https://img-blog.csdnimg.cn/a9658245958d473ab812cebaba84a954.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

尽管这不是介绍自动部署的文章，但我们也打算介绍一下它的主要特征。我们希望我们的软件应该这样方便的工作，因此我们需要更多的自动化测试。流程中工作的软件改进意味着我们能自动的部署到各种新的环境中。

  整体风格的应用相当开心的在各种环境中构建、测试、发布。事实证明，一旦你打算投资一条整体架构应用自动化的的生产线，那么你会发现发布更多的应用似乎非不那么的可怕。记住，CD（持续部署）的一个目标在于让发布变得无趣，因此无论是一个还是三个应用，它都一样的无趣。
另一个方面，我们发现使用微服务的团队更加依赖于基础设施的自动化。相比之下，在整体架构也微服务架构中，尽管发布的场景不同，但发布工作的无趣并没有多大的区别。

![在这里插入图片描述](https://img-blog.csdnimg.cn/ae5ce307c49a49279cdb5de9585647c8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**容错性设计**

使用服务作为组件的一个结果在于应用需要有能容忍服务的故障的设计。任务服务可能因为供应商的不可靠而故障，客户端需要尽可能的优化这种场景的响应。跟整体构架相比，这是一个缺点，因为它带来的额外的复杂性。这将让微服务团队时刻的想到服务故障的情况下用户的体验。Netflix 的Simian Army可以为每个应用的服务及数据中心提供日常故障检测和恢复。

  这种产品中的自动化测试可以让大部分的运维团队正常的上下班。这并不意味着整体构架的应用没有这么精巧的监控配置，只是在我们的经验中它并不常见。

  由于服务可以随时故障，快速故障检测，乃至，自动恢复变更非常重要。微服务应用把实时的监控放在应用的各个阶段中，检测构架元素（每秒数据库的接收的请求数）和业务相关的指标（把分钟接收的定单数）。监控系统可以提供一种早期故障告警系统，让开发团队跟进并调查。
对于微服务框架来说，这相当重要，因为微服务相互的通信可能导致紧急意外行为。许多专家车称赞这种紧急事件的价值，但事实是这种紧急行为有时是灾难。监控是至关重要的，它能快速发现这种紧急不良行为，让我们迅速修复它。

  整体架构，跟微服务一样，在构建时是通明的，实情上，它们就是这样子的。它们不同之处在于，你需要清楚的认识到不同进程间运行的服务是不相关的。库对于同一进程是透明的，也因此不那么重要了。

  微服务团队期望清楚的监控和记录每个服务的配置，比如使用仪表盘显示上/下线状态、各种运维和业务相关的指标。对断路器（circuit breaker）状态、目前的吞吐量和时延细节，我们也会经常遇到。



**设计改进**

微服务实践者，通常有不断改进设计的背景，他们把服务分解成进一步的工具。这些工具可以让应用开发者在不改变速度情况下，控制都他们的应用的需求变更。变更控制不意味首减少变更，而是使用适当的方式和工具，让它更加频繁，至少，很好让它变得可控。

  不论如何，当你试图软件系统拆分成组件时，你将面临着如何拆分的问题。那么我们的决定拆分我们应用的原则是什么呢？首要的因素，组件可以被独立替换和更新的，这意味着我们寻找的关键在于，我们要想象着重写一个组件而不影响它们之前的协作关系。事实上，许多的微服务小组给它进一步的预期：服务应该能够报废的，而不是要长久的发展的。

  Guardian网站就是这方面的一个优秀的例子，它初期被设计和构建成一个整体架构，但它已经向微服务的发展了。整体构架仍然是它网站的核心，但是他们使用微服务来增加那些使用整体架构API的新特性。这种方法增加这些临时的特性非常方便，比如运动新闻的特稿。这样站点的一个部分可以使用快速的开发语言迅速整合起来，当它过时后可以一次性移除。我们发现一家金融机构用相似的方法增加新的市场营销活动，数周或者几个月后把它撤销。

  可代替是模块化开发中的一个特例，它是用模块来应对需要变更的。你希望让变更是相同模块，相同周期中进行变化而已。系统的某些很小做变更部分，也应该放在不同的服务中，这样它们更容易让它们消亡。如果你发现两个服务一直重复的变更时，这就是一个要合并它们的信号了。

  把组件改成服务，增加了细化发布计划的一个机会。整体构架的任务变更需要整个应用的完整的构建和发布。然而，使用微服务，你只需要发布你要修改的服务就可以了。这将简化和加速你的发布周期。缺点是你需要为一个变更服务发布可能中断用户的体验而担心。传统的集成方法是使用版本来处理这些问题，但是微服务版本仅是最后的通告手段。我们需要在设计服务时尽可能的容忍供应商的变更，以避免提供多个版本。



**微服务是未来吗？**

我们写这篇文章的主要目的在于解释微服务的主要思想和原则。但是发时间做这事的时候，我们清醒的认识到微服务构架风格是一个非常重要的想法：一个值得企业应用中认真考虑的东西。我们最近使用这种风格构建了几个系统，认识那些也使用和喜欢这种方法的爱好者。

  我们认识的使用这种方式的先行者，包含亚马逊、Netflix、The Guardian、The UK Government Digital Service、realestate.com.au、Forward和comparethemarket.com。2013看的巡回会议充满了向正在想成为微服务一分子的公司，包含Travis CI。此外，大量的组件正在从事我们认为是微服务的事，只是没有使用微服务的名字而已。（通常，它们被打上SOA的标签，尽管，我们认为SOA有许多不同的地方。）

  尽管有这些积极的经验，然后，我们也不急于确认微服务是未来软件架构方向。至今为止，我们的经验与整体风格的应该中相比出来的是有优势的，但是我们意识知这样的事实，我们并没有足够的时间来证明我们的论证。

  你所使用的架构通常是你开发出来后，使用的几年的实际成果。我们看到这些工程是在一个优秀的团队，带着对模块化的强烈追求，使用在过去几年中已经衰退的整体架构构建出来的。许多人相信，这种衰退不太可能与微服务有关，因为服务边界是清晰的并且很难再完善的。然而，当我们还没看到足够多的系统运行足够长时间时，我们不能肯定微服务构架是成熟的。

  当然，还有原因就是，有人期望微服务构架不够成熟。在组件化方面的任何努力，其成功都依赖于软件如何拆分成适合的组件。指出组件化的准确边界应该在那，这是非常困难的。改良设计要承认边界的权益困境和因此带来的易于重构的重要性。但是当你的组件是被远程通信的服务时，重构比进程内的库又要困难的多。服务边界上的代码迁移是困难的，任务接口的变更需要参与者的共同协作，向后兼容的层次需要被增加，测试也变更更加复杂。

  另一个问题在于，如果组件并没有清晰的划分，你的工作的复杂性将从组件内部转向组件间的关系。做这事不仅要围绕着复杂，它也要面对着不清晰和更难控制的地方。很容易想到，当你在一个小的、简单的组件内找东西，总比在没有关系的混乱的服务间要容易。

  最后，团队技能也是重要的因素。新的技术倾向于被掌握更多的技能的团队使用。但是掌握多技能的团队中使用的技巧在较少技能的团队中并不是必需的。我们发现大量的少技能的团队构建混乱的整合构架，但是它要发时间去证明使用微服务在这种情况下会发生什么。一个糟糕的团队通常开发糟糕的系统：很难说，微服务在这种情况下是否能帮助它们，还是破坏它们。

一个理性的争议在于，我们听说，你不应该从微服务构架开始做。最好从整体构架开发，做模块化开发，然后当整体构架出现问题是再把模块化拆分成服务。（尽管这种建议不是好主意，因为一个好的进程内接口并不是一个好的服务接口。）

  因此我们持这种谨慎的乐观。到目前为止，我们还没有足够认识，关于微构架能否被大范围的推广。我们不能肯定的说，我们要终结什么，但是软件开发的挑战在于你只能在不完整的信息中决定你目前要处理的问题。



**微服务系统多大？**

尽管“微服务”一词在架构风格中越来越流行，它的名字很不辛让人关注它的服务大小，以及对“微”这个组成的争议。在我们与微服务实践者的谈话中，我们发现了服务的大小范围。被报道的最大团队遵循亚马逊Tow Pizaa团队理念（比如，一个团队吃两个比萨就可以了。），这意味着不超过20号（一打）人。我们发现最小配置是半打的团队支撑起一打的服务。

  这也引发这样的考虑：规模为一个服务一打人到一个服务一个人的团队打上微服务的标签。此刻我们认为，它们是一样的，但是随着对这种风格的深入研究，也存在我们改变我们的想法的可能。



**微服务与SOA**

当前我们谈到微服务时，通常会问，这是不是我们20年前讨论的面向服务架构（SOA）。这是一个很好的观点，因为微服务风格也SOA所提倡的一些优势非常相似。尽管如此，问题在于SOA意味的太多不同的东西了，因此通常时候我们谈的所谓“SOA”时，它与我们谈论的风格不一至，因为它通常是指在整体风格应用中的ESB。

  此外，我们发现面向服务的风格是这么的拙劣：从试图使用ESB隐藏复杂性， 到使用多年才认识到发费数百美元却没产生任务价值这样的失败，到集中治理模式抑制变更。而且这些问题往往很难发现。
可以肯定的时，微服务社区中使用的许多的技术都开发者是从大型机构的整合服务经验中发展来的。

  Tolerant Reader模式就是这样的一个例子。由于互联网的发展，利用简单的协议这种方法，让它从这些经验传达的出来。这是从已经很复杂的集中式标准中的一种反模式，坦白的说，真让人惊叹。（无论何时，当你需要用一个服务来管理你的所有的服务，你就知道这很麻烦。）

  SOA的这种常见行为让微服务的提倡者拒绝打上SOA的标签，尽管有人认为微服务是从SOA中发展而来的，或许面向服务是对的。无论如何，事实上SOA表达这么多的含义，它给一个团队清醒的认识到这种构架风格就已经值的了。



**多语言，多选择**

JVM做为一个平台，它的增长就是一个平台中运行多语言的最大的例子。过去二十年中，它通常做为更高层次语言的壳，以达到更高层次的抽象。比如，研究它的内部结构，、使用低级的语言写更高效的代码。尽管如此，许多整体风格并不需要这种层次的性能优化或者在语法及高层次上的抽象，这很常见（让我们很失望）。此外整体构架通常意味着使用单一的语言，这也限制着使用技术的数量。



**实践标准和强制标准**

它有点尴尬，微服务团队倾向于避免这种通常由企业架构队伍定制的僵硬的强制标准，但是它们却非常乐于甚至推广这些开放的标准，如HTTP、ATOM、其它微规范。
关键的不同在这些标准是怎么开发出来的，以及它们是怎么被推广的。标准被一些组件管理，如IETF认证标准，仅当它们在互联网上有几个在用的实现，通常源自于开源工程的成功应用。
这些标准单独分离出来，与那种在企业中通常有没有什么编码经验的或者没有什么影响力的厂商标准进行区别。



**让做对事更容易**

一方面，我们发现在持续发布、部署越来越多的使用自动化，是很多有用的工具开发出来帮助开发者和运营商的努力结果。为打包、代码管理、支撑服务的工具，或者增加标准监控的记录的工具，现在都非常常见了。网络中最好的，可能就是Netflix’s的开源工具，但是包含Dropwizard在内的其它工具也被广泛的使用着。



**断路器(circuit breaker)和产品中现有的代码**

断路器(circuit breaker)出现在《Realease It!》一书中，与Bulkhead和Timeout这样的模式放在一起。实施起来，这些模式用于构建通信应用时相当的重要。Netflix的博客在解释它们的应用时，做了大量的工作。



**同步是有害的**

 任务时候，你在服务间的调用使用同步的方法，都会遇到宕机时间的乘积效应。简单的说，你的系统宕机时间是你系统的单独组件的宕机时间的乘积。你面临的选择使用异步或者管理宕机时间。在www.guardian.co.uk中，它们在新平台中使用一种简单的规则来实现它：在Netflix中每次用户请求的同步调用，他们重新设计的平台API都会把它构建成异步的API来执行。



总结

MVC：三层架构（控制层，业务层，持久层）

MVVM：

**微服务架构：**

1. 微服务架构，把服务拆成了一个个的微服务，就相当于 ssm 开发时的业务。
2. 服务（业务）service：userService：==》模块！ 比如这是用户的业务
3. 但是 服务变成了分布式了，要分布在不同的电脑去放，一台电脑单机放不下了。
4. 怎么办？
5. 是不是这个服务（模块）就得单独放一个电脑了。
6. 所以把服务变成一个模块。
7. 这个服务里面就做这么一件事情
8. SpringMVC 已配置，controller ，微服务负责提供接口：
9. 微服务提供接口，其他电脑就可以用了
10. 有很多很多接口的时候分布在不同电脑上，是不是一个网状的概念，这就是微服务了。
11. 所以微服务不是新东西，只是把我们原来的业务再拆分，拆分成一个个模块。



**官方说法：**
  微服务是一种架构风格，它要求我们在开发一个应用的时候，这个应用必须构建成一系列小服务的组合；可以通过http的方式进行互通。RPC



### 3.2开发演变

随着互联网的发展，网站应用的规模不断扩大，常规的垂直应用架构已无法应对，分布式服务架构以及流动计算架构势在必行，亟需一个治理系统确保架构有条不紊的演进。

![在这里插入图片描述](https://img-blog.csdnimg.cn/0d846b6de23547f4be543b2b813820f0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



**单体应用架构**

1. 是指，我们将一个应用中的所有服务都封装在一个应用中。
2. 无论ERP，CRM或是其他什么系统，你都把数据库访问，web访问，等等各个功能放到一个war包内。
3. 这样做的好处是：易于开发和测试；也十分方便部署；当需要扩展时，只需将war包复制多分，然后4. 放到多个服务器上，再做个负载均衡就可以了。
4. 缺点是：哪怕我要修改一个非常小的地方，我都要停掉整个服务，重新打包、部署整个应用的war包。特别是对于一个大型应用，我们不可能把所有内容都放在一个应用里面，我们如何维护、如果分工合作都是问题



**微服务架构**

5. 把所有的功能单元放在一个应用里面，然后我们整个应用部署到服务器上。如果负载能力不行，我们将整个应用进行水平复制，进行扩展，然后再负载均衡。
6. 所谓微服务架构，就是打破之前单体应用的架构方式，把每个功能元素独立出来。把独立出来的功能元素的动态组合，需要的功能元素才去拿来组合，需要多一些时可以整合多个功能元素。所有微服务是对功能元素进行复制，而没有对整个应用进行复制
7. 这样做的好处是：
8. 节省了调用资源
9. 每个功能元素的服务都是一个可替换的、可独立升级的软件代码。
10. 以下这张 很形象的描述出了 微服务
11. 把每个功能元素独立出来
12. 把独立出来的功能元素的动态组合
13. 需要的功能元素才去拿来组合

![在这里插入图片描述](https://img-blog.csdnimg.cn/57b1a78062834492ba6cb31fbbeedbd1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



用户下单：controller 1s
  仓库冻结：资金冻结：验证：购买成功，仓库数量减少，仓库解冻，服务解冻，资金解冻 10s

程序：高内聚，低耦合

文章推荐
原文：https://martinfowler.com/articles/microservices.html
论文：https://www.cnblogs.com/liuning8023/p/4493156.html



### 3.3如何构建微服务

一个大型的微服务架构，就像一个复杂交织的神经网络，每一个神经元就是一个功能元素，他们各自完成注解的功能，然后通过http相互请求调用。

  比如一个电商系统，查缓存、连数据库、浏览页面、结账、支付等服务都是一个个独立的功能服务，都被微化了，它们作为一个个微服务共同构建了一个庞大的系统。修改其中的一个功能，只需升级其中一个功能服务单元即可。

  但是这种庞大的系统架构给部署和运维带来很大的难度。于是，Spring为我们带来了构建大型分布式微服务的全套、全程产品



## 4.第一个SpringBoot程序

```http
官网：https://spring.io/projects/spring-boot
```



版本

![在这里插入图片描述](https://img-blog.csdnimg.cn/9ef854584ceb4b2e8f9c7529ab975125.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



官方提供一个快速构建项目的网站
https://start.spring.io/

![在这里插入图片描述](https://img-blog.csdnimg.cn/8747cf8b5671411286fd0684b6202c88.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



构建Spring boot 项目 添加web 依赖

![在这里插入图片描述](https://img-blog.csdnimg.cn/202e5c676a0b404fa75d9d0b81be87b5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



下载

![在这里插入图片描述](https://img-blog.csdnimg.cn/1336a0aff51544f48f85cef6b7de32f9.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





Spring boot 默认结构

![在这里插入图片描述](https://img-blog.csdnimg.cn/55ccf3747ea44c8fb19f9d2745d79005.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



直接使用idea 创建一个Spring Boot项目（一般开发直接在idea创建）

spring-boot-starter 所有的Springboot 依赖都是使用这个开头的

```xml
<!--web 依赖 tomcat，dispatcherServlet，xml 都没有了-->
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>

```

```xml
<!--单元测试-->
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-test</artifactId>
   <scope>test</scope>
</dependency>

```

```xml
<!--打jar 包插件-->
<plugins>
   <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>
   </plugin>
</plugins>

```



### 4.1修改启动时的Logo

只需一步：到项目下的 resources 目录下新建一个banner.txt 即可。
图案可以到：https://www.bootschool.net/ascii 这个网站生成，然后拷贝到文件中即可！

```tex

//                          _ooOoo_                               //
//                         o8888888o                              //
//                         88" . "88                              //
//                         (| ^_^ |)                              //
//                         O\  =  /O                              //
//                      ____/`---'\____                           //
//                    .'  \\|     |//  `.                         //
//                   /  \\|||  :  |||//  \                        //
//                  /  _||||| -:- |||||-  \                       //
//                  |   | \\\  -  /// |   |                       //
//                  | \_|  ''\---/''  |   |                       //
//                  \  .-\__  `-`  ___/-. /                       //
//                ___`. .'  /--.--\  `. . ___                     //
//              ."" '<  `.___\_<|>_/___.'  >'"".                  //
//            | | :  `- \`.;`\ _ /`;.`/ - ` : | |                 //
//            \  \ `-.   \_ __\ /__ _/   .-` /  /                 //
//      ========`-.____`-.___\_____/___.-`____.-'========         //
//                           `=---='                              //
//      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^        //
//            佛祖保佑       永不宕机     永无BUG                    //


```

![在这里插入图片描述](https://img-blog.csdnimg.cn/d4e0dbb31cae4d32862e06d1f71fb85e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 4.2Idea 创建SpringBoot项目

选择Spring Initalizr

![在这里插入图片描述](https://img-blog.csdnimg.cn/574fd172639747429d9e9d87eb178711.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



选择版本

![在这里插入图片描述](https://img-blog.csdnimg.cn/ea704643d9394dc59b193c73b222be49.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





选择要添加的依赖

![在这里插入图片描述](https://img-blog.csdnimg.cn/07a84c30512d4d5e80f492082d7d3179.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)





设置项目名

![在这里插入图片描述](https://img-blog.csdnimg.cn/c5f195abdc524479966303f49ec73d99.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



编写一个Controller测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/d289da9a440f4c7dbf7e5210a653bd5d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/f700c19c88ee4f37b91d45662100e16c.png#pic_center)



## 5.SpringBoot 自动装配原理

https://blog.csdn.net/qq_42025798/article/details/122058013



## 6.Yml

### 6.1 yml 语法

    SpringBoot使用一个全局的配置文件 ， 配置文件名称是固定的

```xml
application.properties
    语法结构 ：key=value
application.yml
    语法结构 ：key：空格 value

```



配置文件的作用 ：修改SpringBoot自动配置的默认值，因为SpringBoot在底层都给我们自动配置好了；

比如我们可以在配置文件中修改Tomcat 默认启动的端口号！测试一下！
server:
port: 8081



**yaml概述**
  YAML是 “YAML Ain’t a Markup Language” （YAML不是一种标记语言）的递归缩写。在开发的这种语言时，YAML 的意思其实是：“Yet Another Markup Language”（仍是一种标记语言）
这种语言以数据作为中心，**而不是以标记语言为重点**！
以前的配置文件，大多数都是使用xml来配置；比如一个简单的端口配置，我们来对比下yaml和xml

**传统xml配置：**

```xml
<server>    
     <port>8081<port>
</server>

```



**yaml配置：**

```yaml
server:
  port: 8081

```



**properties 和yml 对比**
  yml可以注入到我们的配置类中

![在这里插入图片描述](https://img-blog.csdnimg.cn/8442277cc6824c0ead8226ad913fd254.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



yml 使用 **对象、Map**（键值对）

```yaml
#对象、Map格式
k:     v1:    
  	   v2:

```



### 6.2.yml 直接注入匹配值

1、在springboot项目中的resources目录下新建一个文件 application.yml

2、编写一个实体类 Dog；

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component
public  class Dog {
    private String name;
    private Integer age;
}

```



3、编写一个实体类 Person；

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component
@ConfigurationProperties(prefix = "person")
public class Person {
    private String name;
    private Integer age;
    private Boolean happy;
    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
}

```



4、在yml文件中配置person类

```yaml
person:
  name: xy
  age: 18
  happy: false
  birth: 2021/5/3
  maps:
    k1: v1
    k2: v2
  lists:
    - code
    - music
    - girl
  dog:
    name: 旺财
    age: 3

```



5、测试

```java
@Test
void contextLoads() {undefined
System.out.println(person);
}
```



6、结果

```java
Person(name=xy, age=18, happy=false, birth=Mon May 03 00:00:00 CST 2021, maps={k1=v1, k2=v2}, lists=[code, music, girl], dog=Dog{name='旺财', age=3})

```



IDEA 提示，springboot配置注解处理器没有找到，让我们看文档，我们可以查看文档，找到一个依赖！

![在这里插入图片描述](https://img-blog.csdnimg.cn/dec395320b824a21b5b610a6816ff1da.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

```xml
<!-- 导入配置文件处理器，配置文件进行绑定就会有提示，需要重启 -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>

```



`@ConfigurationProperties` 作用：

1. 将配置文件中的每一个属性的值，映射到这个组件中
2. 告诉SpringBoot将类中的所有属性和配置文件中相关的配置进行绑定
3. 参数：
4. prefix “person” ：将配置文件中的person 下面的所有属性一一定义
5. 只有这个组件是容器中的组件，才能使用容器提供的@ConfigurationProperties功能



**@PropertySource注解**
用于加载指定的配置文件

```java
dog类
@Component
@NoArgsConstructor
@AllArgsConstructor
@Data
@PropertySource(value = "classpath:xy.properties")
public  class Dog {
    //SPEL表达式读取配置文件的值
    @Value("${dog.name}")
    private String name;
    @Value("${dog.age}")
    private Integer age;
}

```



xy.properties文件

```properties
dog.name=旺财
dog.age=3

```



测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/7d1f6da6e92c4adfb4eb15fe618c936c.png#pic_center)

properties配置文件在写中文的时候，会有乱码 ， 我们需要去IDEA中设置编码格式为UTF-8；

![在这里插入图片描述](https://img-blog.csdnimg.cn/7bc51021efbf4204a26b8a9b09c27ceb.png#pic_center)



对比小结：
`@Value`这个使用起来并不友好！我们需要为每个属性单独注解赋值

`@ConfigurationProperties`只需要写一次即可 ， `@Value`则需要每个字段都添加
松散绑定：这个什么意思呢? 比如我的yml中写的last-name，这个和lastName是一样的， - 后面跟着的字母默认是大写的。这就是松散绑定。可以测试一下
JSR303数据校验 ， 这个就是我们可以在字段是增加一层过滤器验证 ， 可以保证数据的合法性
复杂类型封装，yml中可以封装对象 ， 使用value就不支持



**松散绑定**
dog类

```java
@Component
@NoArgsConstructor
@AllArgsConstructor
@Data
@ConfigurationProperties(prefix = "dog")
public  class Dog {
    private String firstName;
    private Integer age;
}

```



yml文件

```yaml
dog:
  first-name: 来福
  age: 3
测试类
    @Test
    void contextLoads() {
        System.out.println(dog);
    }

```



结果

```tex
Dog(firstName=来福, age=3)

```



结论：

1. 配置yml和配置properties都可以获取到值 ， 强烈推荐 yml；
2. 如果我们在某个业务中，只需要获取配置文件中的某个值，可以使用一下 @value；
3. 如果说，我们专门编写了一个JavaBean来和配置文件进行一一映射，就直接`@configurationProperties`，不要犹豫！



### 6.3JSR303数据校验

Springboot中可以用@validated来校验数据，如果数据异常则会统一抛出异常，方便异常中心统一处理。我们这里来写个注解让我们的name只能支持Email格式；

JSR 303 基本的校验规则

空检查
  `@Null` 验证对象是否为null
  `@NotNull` 验证对象是否不为null, 无法查检长度为0的字符串
  `@NotBlank` 检查约束字符串是不是Null还有被Trim的长度是否大于0,只对字符串,且会去掉前后空格.
  `@NotEmpty` 检查约束元素是否为NULL或者是EMPTY.



**Booelan检查**
  `@AssertTrue` 验证 Boolean 对象是否为 true
  `@AssertFalse` 验证 Boolean 对象是否为 false



**长度检查**
  `@Size(min=, max=)` 验证对象（Array,Collection,Map,String）长度是否在给定的范围之内
  `@Length(min=, max=)` Validates that the annotated string is between min and max included.



**日期检查**
  `@Past` 验证 Date 和 Calendar 对象是否在当前时间之前，验证成立的话被注释的元素一定是一个过去的日期
  `@Future` 验证 Date 和 Calendar 对象是否在当前时间之后 ，验证成立的话被注释的元素一定是一个将来的日期
  `@Pattern` 验证 String 对象是否符合正则表达式的规则，被注释的元素符合制定的正则表达式，regexp:正则表达式 flags: 指定 Pattern.Flag 的数组，表示正则表达式的相关选项。



**数值检查**
建议使用在Stirng,Integer类型，不建议使用在int类型上，因为表单值为“”时无法转换为int，但可以转换为Stirng为”“,Integer为null

  `@Min` 验证 Number 和 String 对象是否大等于指定的值
  `@Max` 验证 Number 和 String 对象是否小等于指定的值
  `@DecimalMax` 被标注的值必须不大于约束中指定的最大值. 这个约束的参数是一个通过BigDecimal定义的最大值的字符串表示.小数存在精度
  `@DecimalMin `被标注的值必须不小于约束中指定的最小值. 这个约束的参数是一个通过BigDecimal定义的最小值的字符串表示.小数存在精度
  `@Digits` 验证 Number 和 String 的构成是否合法
  `@Digits(integer=,fraction=)` 验证字符串是否是符合指定格式的数字，interger指定整数精度，fraction指定小数精度。
  `@Range(min=, max=) `被指定的元素必须在合适的范围内
  `@Range`(min=10000,max=50000,message=”range.bean.wage”)
  `@Valid` 递归的对关联对象进行校验, 如果关联对象是个集合或者数组,那么对其中的元素进行递归校验,如果是一个map,则对其中的值部分进行校验.(是否进行递归验证)
  `@CreditCardNumber`信用卡验证
  `@Email` 验证是否是邮件地址，如果为null,不进行验证，算通过验证。
  `@ScriptAssert`(lang= ,script=, alias=)
  `@URL`(protocol=,host=, port=,regexp=, flags=)

person类

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
@Component
@ConfigurationProperties(prefix = "person")
@Validated//数据校验
public class Person {

    @NotNull
    private String name;

    private Integer age;
    private Boolean happy;
    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
}

```



yml 文件

```yaml
person:
  age: 18
  happy: false
  birth: 2021/5/3
  maps:
    k1: v1
    k2: v2
  lists:
    - code
    - music
    - girl
  dog:
    name: 旺财
    age: 3

```



测试

```java
@Test
void contextLoads() {undefined
System.out.println(person);
}
```



测试结果：
  我的name数据为赋值，所以为null，验证不通过，抛出异常

![在这里插入图片描述](https://img-blog.csdnimg.cn/089df09e53974425ac53a4249aba3634.png#pic_center)



### 6.4.多环境配置及配置文件位置

SpringBoot会从这四个位置全部加载主配置文件；互补配置；
  优先级1：**项目路径**下的**config**文件夹配置文件
  优先级2：**项目路径**下配置文件
  优先级3：**资源路径**下的**config**文件夹配置文件
  优先级4：**资源路径**下配置文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/54ad1e3ccaec4d5f9f92363d0a4294bc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_14,color_FFFFFF,t_70,g_se,x_16#pic_center)



**多配置文件**
  我们在主配置文件编写的时候，文件名可以是 **application-**{profile}.properties/yml , 用来指定多个环境版本；

![在这里插入图片描述](https://img-blog.csdnimg.cn/078b4ff220f2442d8f8891b993ad42a2.png#pic_center)



```yaml
#比如在配置文件中指定使用dev环境，我们可以通过设置不同的端口号进行测试；
#我们启动SpringBoot，就可以看到已经切换到dev下的配置了；
spring:
  profiles:
    active: dev

```



## 7.web开发探究

### 7.1静态资源导入探究

19.静态资源导入探究
注意研究对象：WebMVCAutoConfiguration 类

研究方法 `public void addResourceHandlers(ResourceHandlerRegistry registry)`

1. webjars
2. 找到webjars官网 https://www.webjars.org/
3. 找到maven方式导入依赖

![在这里插入图片描述](https://img-blog.csdnimg.cn/21cea31d68be46de81745983fe129583.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



在pom.xml文件中引入
找到jquery

![在这里插入图片描述](https://img-blog.csdnimg.cn/02fa4d43966644e88b60ac2bb6f6acf8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_19,color_FFFFFF,t_70,g_se,x_16#pic_center)

```java
//如果有自动配置就失效了
@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    //如果这个静态资源的东西已经被自定义了，直接return
   if (!this.resourceProperties.isAddMappings()) {
      logger.debug("Default resource handling disabled");
      return;
   }
   Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
   CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
   //能找到静态资源的地方
     if (!registry.hasMappingForPattern("/webjars/**")) {
      customizeResourceHandlerRegistration(registry.addResourceHandler("/webjars/**")
            .addResourceLocations("classpath:/META-INF/resources/webjars/")
            .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
   }
   //第二种，获取静态资源的路径
   String staticPathPattern = this.mvcProperties.getStaticPathPattern();
   if (!registry.hasMappingForPattern(staticPathPattern)) {
      customizeResourceHandlerRegistration(registry.addResourceHandler(staticPathPattern)
            .addResourceLocations(getResourceLocations(this.resourceProperties.getStaticLocations()))
            .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
   }
}

```



以上是去webjars 中找静态资源（第一种）很少使用

```http
http://localhost:8080/webjars/jquery/3.6.0/jquery.js

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b2ef783c09b4400eaf88ab4fd4a06bbc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



第二种

![在这里插入图片描述](https://img-blog.csdnimg.cn/a1a0c0024ce0494fa34a41969830eced.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/f534363e50894733940a198c93c1f284.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/35b9b55c90e642fb83030923392f6d3b.png#pic_center)

1. classpath:`/META-INF/resources/`
2. classpath:`/resources/` 优先级第一
3. classpath:`/static/` 优先级第二
4. classpath:`/public/` 优先级第三

```http
http://localhost:8080/**

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/b7a93392b63f48b8a65a442324ca0a80.png#pic_center)



### 7.2首页如何定制

20.首页如何定制

注意研究对象：WebMVCAutoConfiguration 类

![在这里插入图片描述](https://img-blog.csdnimg.cn/540863f74ddb4e7194e930c8cd51d4e7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)

1. 在静态资源目录下 定义 名称为`index.html` 文件即可。
2. 但是一般我们不这么做，我们都是放在`template 目录`下
3. 然后通过`controller 跳转`的
4. 访问template 目录下必须`导入thymeleaf 依赖`

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/323822a0890c44159788d7f74a794876.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 7.3Thymeleaf使用

  前端交给我们的页面，是html页面。如果是我们以前开发，我们需要把他们转成jsp页面，jsp好处就是当我们查出一些数据转发到JSP页面以后，我们可以用jsp轻松实现数据的显示，及交互等。

  jsp支持非常强大的功能，包括能写Java代码，但是呢，我们现在的这种情况，SpringBoot这个项目首先是以jar的方式，不是war，像第二，我们用的还是嵌入式的Tomcat，所以呢，他`现在默认是不支持jsp的`。

  那不支持jsp，如果我们直接用纯静态页面的方式，那给我们开发会带来非常大的麻烦，那怎么办呢？

**SpringBoot推荐你可以来使用模板引擎**：

 模板引擎，我们其实大家听到很多，其实jsp就是一个模板引擎，还有用的比较多的freemarker，包括SpringBoot给我们推荐的Thymeleaf，模板引擎有非常多，但再多的模板引擎，他们的思想都是一样的，什么样一个思想呢我们来看一下这张图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/d15d21fdfadb41df9102c0176e9389ba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



模板引擎的作用就是我们来写一个页面模板，比如有些值呢，是动态的，我们写一些表达式。
而这些值，从哪来呢，就是我们在后台封装一些数据。然后把这个模板和这个数据交给我们模板引擎，模板引擎按照我们这个数据帮你把这表达式解析、填充到我们指定的位置，然后把这个数据最终生成一个我们想要的内容给我们写出去，这就是我们这个模板引擎，不管是jsp还是其他模板引擎，都是这个思想。

 只不过呢，就是说不同模板引擎之间，他们可能这个语法有点不一样。

 SpringBoot给我们推荐的Thymeleaf模板引擎，这模板引擎呢，是一个高级语言的模板引擎，他的这个语法更简单。而且呢，功能更强大。

引入Thymeleaf
1.导入依赖

```xml
<!-- 引入thymeleaf-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>

```



2.编写controller

```java
@Controller
public class ThymeleafController {

    @RequestMapping("thymeleaf/test1")
    public String test1(Model model){
        model.addAttribute("msg","hello thymeleaf");
        return "test1";
    }
}

```



3.在html页面引入thymeleaf 名称空间

```html
<html lang="en" xmlns:th="http://www.thymeleaf.org">

```



4.编写html页面

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>test1</h1>
<!--取出值-->
<p th:text="${msg}"></p>

</body>
</html>

```



5.测试

```http
http://localhost:8080/thymeleaf/test1

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/dee7190bfce240b0a0898b0d9e6b9473.png#pic_center)



Thymeleaf语法规则

![在这里插入图片描述](https://img-blog.csdnimg.cn/de4847df4c3b4d30a42dafea970af898.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



### 7.4Thymeleaf 遍历

**普通字符串**

```java
@RequestMapping("thymeleaf/test1")
public String test1(Model model){
    model.addAttribute("msg","hello thymeleaf");
    return "test1";
}

<p th:if="${msg == null}">
    没有数据
</p>
<p th:if="${msg != null}">
    <p th:text="${msg}"></p>
</p>

```



**获取对象**

```java
@RequestMapping("thymeleaf/test4")
public String test4(Model model){
    model.addAttribute("user",new User(1,"闲言",18));
    return "test1";
}

<p th:if="${user != null}">
    <p th:text="${user.id}"></p>
    <p th:text="${user.name}"></p>
    <p th:text="${user.age}"></p>
</p>

```



**遍历 list**

```java
@RequestMapping("thymeleaf/test2")
public String test2(Model model){
    List<String> lists = new ArrayList<>();
    lists.add("Jsp");
    lists.add("SpringBoot");
    lists.add("Spring");
    lists.add("JavaSE");
    model.addAttribute("lists",lists);
    return "test1";
}

<table border="1">
    <tr>
        <th>Name</th>
    </tr>
    <tr th:each="list : ${lists}">
        <td th:text="${list}"></td>
    </tr>
</table>

```



**遍历map**

```java
@RequestMapping("thymeleaf/test3")
public String test3(Model model){

    Map<String,Object> maps = new HashMap<>();
    maps.put("闲言","csdn闲言");
    maps.put("k2","v2");
    maps.put("k3","v3");
    maps.put("k4","v4");

    model.addAttribute("maps",maps);
    return "test1";
}

<table class="layui-table">
    <tr th:each="item,map:${maps}">
        <td th:text="${map.index}+1"></td>
        <td th:text="${map.current.key}"></td><!-- key-->
        <td th:text="${map.current.value}"></td><!-- value-->
    </tr>
</table>

```



### 7.5Thymeleaf 练习

```http
<html lang="en" xmlns:th="http://www.thymeleaf.org">

```



在模板引擎引入css样式 `@{/css/bootstrap.min.css}`

```css
<link th:href="@{/css/bootstrap.min.css}" rel="stylesheet">

```



引入图片样`式 @{/img/bootstrap-solid.svg}`

```html
<img class="mb-4" th:src="@{/img/bootstrap-solid.svg}" alt="" width="72" height="72">

```



国际化引入 `#{login.tip}`

```html
<h1 class="h3 mb-3 font-weight-normal" th:text="#{login.tip}">Please sign in</h1>

```



配置国际化，因为button 标签比较特殊 不能通过 th:value="${}" 配置
需要使用[[ #{ }]]

```html
<button class="btn btn-lg btn-primary btn-block" type="submit" >[[#{login.btn}]]</button>

<input type="text" class="form-control" th:placeholder="#{login.username}" required="" autofocus="">
<label class="sr-only">Password</label>
<input type="password" class="form-control" th:placeholder="#{login.password}" required="">

```



**thymeleaf 提取公共页面**
th:fragment=“sidebar”

```jsp

<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">

<!--头部导航栏-->
<nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0" th:fragment="navbar">
    <a class="navbar-brand col-sm-3 col-md-2 mr-0" href="http://getbootstrap.com/docs/4.0/examples/dashboard/#">[[${session.loginUser}]]</a>
    <input class="form-control form-control-dark w-100" type="text" placeholder="Search" aria-label="Search">
    <ul class="navbar-nav px-3">
        <li class="nav-item text-nowrap">
            <a class="nav-link" href="#">注销</a>
        </li>
    </ul>
</nav>


<!--侧边栏-->
<!--th:fragment="sidebar" 将责编了抽取出来，名称为 sidebar -->
<nav class="col-md-2 d-none d-md-block bg-light sidebar" th:fragment="sidebar">

    <div class="sidebar-sticky">
        <ul class="nav flex-column">
            <li class="nav-item">
                <a class="nav-link active" th:href="@{/index}">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-home">
                        <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                        <polyline points="9 22 9 12 15 12 15 22"></polyline>
                    </svg>
                    首页<span class="sr-only">(current)</span>
                </a>
            </li>
            <li class="nav-item">
                <a class="nav-link" th:href="@{/employees/list}">
                    员工管理
                </a>
            </li>
        </ul>
    </div>
</nav>

</html>

```





**使用公共页面**
th:replace="~{commons/commons.html::navbar}

```html
<div th:replace="~{commons/commons.html::navbar}"></div>

```



## 8.使用国际化

1.配置i18n 文件

![在这里插入图片描述](https://img-blog.csdnimg.cn/7f2df3df7d6e4503b3db3485ff5dccb7.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/6cd9a1bf84e544ae98a191c21de39491.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



前台页面使用

![在这里插入图片描述](https://img-blog.csdnimg.cn/500d4b31b7c749f4ab4920beeb694d31.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



2.如果需要在项目中进行按钮自动切换，需要自定义一个组件，并将其注入Spring容器

![在这里插入图片描述](https://img-blog.csdnimg.cn/4169591528dc4c2983eaa29b3fb043ab.png#pic_center)



```java
public class MyLocalResolver implements LocaleResolver {

    /**
     * 解析请求
     * @param request
     * @return
     */
    @Override
    public Locale resolveLocale(HttpServletRequest request) {
        //获取请求中的语言参数
        String language = request.getParameter("l");
        //如果没有就使用默认的
        Locale locale = Locale.getDefault();
        if (!StringUtils.isEmpty(language)){
            String[] split = language.split("_");
            //国家-地区
            locale =  new Locale(split[0], split[1]);
        }

        return locale;
    }

    @Override
    public void setLocale(HttpServletRequest request, HttpServletResponse response, Locale locale) {

    }
}

```

```java
/**
 * 自定义的国际化组件
 * @return
 */
@Bean
public LocaleResolver localeResolver(){
    return new MyLocalResolver();
}

```





## 9.整合JDBC

### 9-1.导入依赖

```xml
<dependencies>
    <!--jdbc-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jdbc</artifactId>
    </dependency>
    <!--mysql 驱动-->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
    <!--lombok插件-->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
    <!--测试相关-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>

```



### 9-2.编写yaml配置文件连接数据库

```yaml
spring:
  datasource:
    #?serverTimezone=UTC解决时区的报错
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    username: root
    password: 123
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      auto-commit: false

```



### 9-3.测试

```java
@SpringBootTest
class SpringBootDemo02JdbcApplicationTests {

    @Autowired
    DataSource dataSource;

    @Test
    void contextLoads() throws Exception{
        //默认数据源：class com.zaxxer.hikari.HikariDataSource
        System.out.println(dataSource.getClass());
        //获取数据库连接
        Connection connection = dataSource.getConnection();
        //是否自动提交事务
        boolean autoCommit = connection.getAutoCommit();
        System.out.println(autoCommit);
        connection.commit();
    }

}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/9f85b14035b94cf6af04046820288051.png)





## 10.整合Druid

Java程序很大一部分要操作数据库，为了提高性能操作数据库的时候，又不得不使用**数据库连接池。**

  **Druid** 是阿里巴巴开源平台上一个数据库连接池实现，结合了 C3P0、DBCP 等 DB 池的优点，同时加入了日志监控。

  Druid 可以很好的监控 DB 池连接和 SQL 的执行情况，天生就是针对监控而生的 DB 连接池。

  Druid已经在阿里巴巴部署了超过600个应用，经过一年多生产环境大规模部署的严苛考验。

  Spring Boot 2.0 以上默认使用 Hikari 数据源，可以说 Hikari 与 Driud 都是当前 Java Web 上最优秀的数据源，我们来重点介绍 Spring Boot 如何集成 Druid 数据源，如何实现数据库监控。



### 1、导入依赖

```xml
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
        <!--druid依赖-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.21</version>
        </dependency>
        <!--mysql依赖-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <!--lombok插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <!--测试-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

```



### 2、配置yml文件

  Spring Boot 2.0 以上默认使用 com.zaxxer.hikari.HikariDataSource 数据源，但可以 通过 spring.datasource.type 指定数据源。

```yaml
# 配置数据库
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    password: 123
    username: root
    # 切换数据源
    type: com.alibaba.druid.pool.DruidDataSource



```



### 3.添加配置类

  现在需要程序员自己为 DruidDataSource 绑定全局配置文件中的参数，再添加到容器中，而不再使用 Spring Boot 的自动生成了；我们需要 自己添加 DruidDataSource 组件到容器中，并绑定属性；

```java
@Configuration
public class DruidConfig {

    private int maxActive;

    /*
       将自定义的 Druid数据源添加到容器中，不再让 Spring Boot 自动创建
       绑定全局配置文件中的 druid 数据源属性到 com.alibaba.druid.pool.DruidDataSource从而让它们生效
       @ConfigurationProperties(prefix = "spring.datasource")：作用就是将 全局配置文件中
       前缀为 spring.datasource的属性值注入到 com.alibaba.druid.pool.DruidDataSource 的同名参数中
    */
    @Bean
    public DataSource druidDataSource(){

        return new DruidDataSource();
    }

}

```



### 4、测试

#### 4.1测试默认参数

```java
@SpringBootTest
class SpringBootDemo04DruidApplicationTests {

    @Autowired
    private DataSource dataSource;

    @Test
    void contextLoads() throws Exception{
        System.out.println(dataSource.getClass()) ;


        DruidDataSource data = (DruidDataSource) dataSource;
        System.out.println("DruidDatasource 最大连接数"+data.getMaxActive());
        System.out.println("DruidDataSource 初始化连接数"+data.getInitialSize());
    }

}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/87feaf64d15e42f08f855e49316bd7d0.png)



#### 4.2测试修改后的参数

在yml文件中修改参数

最终的yml文件如下

```yaml
# 配置数据库
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    password: 123
    username: root
    # 切换数据源
    type: com.alibaba.druid.pool.DruidDataSource
    #Spring Boot 默认是不注入这些属性值的，需要自己绑定
    #druid 数据源专有配置
    initialSize: 5
    MaxActive: 20
    

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/52c10023bd2743d2958f99f1238b3938.png)



### 5、配置Druid数据源监控

  Druid 数据源具有监控的功能，并提供了一个 web 界面方便用户查看，类似安装 路由器 时，人家也提供了一个默认的 web 页面。

  所以第一步需要设置 Druid 的后台管理页面，比如 登录账号、密码 等；配置后台管理；

```java
//配置 Druid 监控管理后台的Servlet；
//内置 Servlet 容器时没有web.xml文件，所以使用 Spring Boot 的注册 Servlet 方式
    @Bean
    public ServletRegistrationBean statViewServlet() {
        ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");

        // 这些参数可以在 com.alibaba.druid.support.http.StatViewServlet
        // 的父类 com.alibaba.druid.support.http.ResourceServlet 中找到
        Map<String, String> initParams = new HashMap<>();
        initParams.put("loginUsername", "admin"); //后台管理界面的登录账号
        initParams.put("loginPassword", "123456"); //后台管理界面的登录密码

        //后台允许谁可以访问
        //initParams.put("allow", "localhost")：表示只有本机可以访问
        //initParams.put("allow", "")：为空或者为null时，表示允许所有访问
        initParams.put("allow", "");
        //deny：Druid 后台拒绝谁访问
        //initParams.put("kuangshen", "192.168.1.20");表示禁止此ip访问

        //设置初始化参数
        bean.setInitParameters(initParams);
        return bean;
    }

```

配置完毕后，我们可以选择访问 ：http://localhost:8080/druid/login.html

![在这里插入图片描述](https://img-blog.csdnimg.cn/4de8e5ee934340ddaac33093533161ce.png)



进入之后

![在这里插入图片描述](https://img-blog.csdnimg.cn/f530669c3b944dc1b6d47e5cd63846aa.png)



### 6、配置 Druid web 监控 filter 过滤器

```java
//配置 Druid 监控 之  web 监控的 filter
//WebStatFilter：用于配置Web和Druid数据源之间的管理关联监控统计
@Bean
public FilterRegistrationBean webStatFilter() {
    FilterRegistrationBean bean = new FilterRegistrationBean();
    bean.setFilter(new WebStatFilter());

    //exclusions：设置哪些请求进行过滤排除掉，从而不进行统计
    Map<String, String> initParams = new HashMap<>();
    initParams.put("exclusions", "*.js,*.css,/druid/*,/jdbc/*");
    bean.setInitParameters(initParams);

    //"/*" 表示过滤所有请求
    bean.setUrlPatterns(Arrays.asList("/*"));
    return bean;
}

```



完整的Druid配置类

```yaml
server:
  port: 808
# 配置数据库
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    password: 123
    username: root
    # 切换数据源
    type: com.alibaba.druid.pool.DruidDataSource
    #Spring Boot 默认是不注入这些属性值的，需要自己绑定
    #druid 数据源专有配置
    #Spring Boot 默认是不注入这些属性值的，需要自己绑定
    #druid 数据源专有配置
    initialSize: 5
    minIdle: 5
    maxActive: 20
    maxWait: 60000
    timeBetweenEvictionRunsMillis: 60000
    minEvictableIdleTimeMillis: 300000
    validationQuery: SELECT 1 FROM DUAL
    testWhileIdle: true
    testOnBorrow: false
    testOnReturn: false
    poolPreparedStatements: true

    #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
    #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
    #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
    filters: stat,wall,log4j
    maxPoolPreparedStatementPerConnectionSize: 20
    useGlobalDataSourceStat: true
    connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500



```





## 11.整合Mybatis

### 1.导入依赖

[mybatis](https://so.csdn.net/so/search?q=mybatis&spm=1001.2101.3001.7020)-spring-boot-starter 不是springboot官方的，自研的

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
        <!--mysql-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <!--lombox插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <!--测试-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--jdbc-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jdbc</artifactId>
        </dependency>
        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.4</version>
        </dependency>
    </dependencies>

```



### 2.在启动类配置包扫描

```java
@SpringBootApplication
@MapperScan(basePackages = {"cn.bloghut.mapper"})
public class MybatisApplication {

    public static void main(String[] args) {
        SpringApplication.run(MybatisApplication.class, args);
    }

}

```



### 3.配置yml文件

```yaml
# 配置数据库
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://localhost:3306/mybatis?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    password: 123
    username: root
# 配置Mybatis
mybatis:
  # 配置实体类别名
  type-aliases-package: cn.bloghut.pojo
  # 配置映射文件路径
  mapper-locations: classpath:cn/bloghut/mapper/*.Mapper.xml

```



### 4.编写用户类，用于封装查询出来的数据

```java
@Data
public class User {
    private int id;
    private String username;
    private String pwd;
}

```



### 5.编写Mapper接口

```java
@Repository
public interface UserMapper {

    List<User> findAll();

}

```



### 6.编写Mapper映射文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.bloghut.mapper.UserMapper">

    <select id="findAll" resultType="User">
        select * from users
    </select>
</mapper>

```



### 7.测试

```java
@SpringBootTest
class SpringbootBootDemo03MybatisApplicationTests {

    @Autowired
    private UserMapper userMapper;

    @Test
    void contextLoads() {
        List<User> users = userMapper.findAll();
        for (User user : users){
            System.out.println(user);
        }
    }

}

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/da75d517b47b44cb88c6d2b0c6f87681.png)



## 12.整合Swagger

### 1.导入依赖

```xml
 <!--web依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <!--springboot测试依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <!--Swagger依赖-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.9.2</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.9.2</version>
        </dependency>
        <!--lombox 插件-->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>

```



### 2.创建[Swagger](https://so.csdn.net/so/search?q=Swagger&spm=1001.2101.3001.7020)配置类

```java
package cn.bloghut.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.service.VendorExtension;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

import java.util.ArrayList;

/**
 * @Classname SwrggerConfig
 * @Description TODO
 * @Date 2021/12/16 15:11
 * @Created by 闲言
 */
@EnableSwagger2
@Configuration
public class SwaggerConfig {
    /**
     * 配置Swagger docket 的 bean 例
     * @return
     */
    @Bean
    public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()//RequestHandlerSelectors 配置要扫描解接口的方式
                //basePackage 指定要扫描的包
                //any()：扫描全部
                //none():不扫码
                //withClassAnnotation：扫描类上的注解，参数是注解的反射对象
                //withMethodAnnotation：扫描方法上的注解
                //withClassAnnotation(RestController.class) 只会扫描类上有RestController 注解的类
                .apis(RequestHandlerSelectors.basePackage("cn.bloghut.controller"))
                //paths()   过滤路径
                .paths(PathSelectors.ant("/**"))
                .build();
    }

    /**
     * 单独抽取出来
     * @return
     */
    public ApiInfo apiInfo(){
    
        Contact contact = new Contact("闲言","http://www.bloghut.cn","1765736057@qq.com");

        return new ApiInfo(
                "闲言的Swagger Api 文档",
                "即使再小的帆也能远航",
                "v1.0",
                "http://www.bloghut.cn",
                contact,
                "Apache 2.0",
                "http://www.apache.org/licenses/LICENSE-2.0",
                new ArrayList<VendorExtension>());

    }
}


```





### 3.创建实体类

```java
/**
 * @Classname User
 * @Description 老师实体类
 * @Date 2021/12/16 15:29
 * @Created by 闲言
 */
@Data
@ApiModel("老师实体类")
@Api("注释信息")
public class User {
    @ApiModelProperty("用老师D")
    private int id;
    @ApiModelProperty("老师名")
    private String name;
}

```



### 4.编写控制器

```java
/**
 * @Classname TeacherController
 * @Description 老师控制器
 * @Date 2021/12/16 15:19
 * @Created by 闲言
 */
@RestController
@RequestMapping("teacher")
public class TeacherController {

    @GetMapping("findAll")
    @ApiOperation("方法注释查询所有老师方法")
    public Object findAll(){
        return "Hello SpringBoot!";
    }

    @PostMapping("add")
    @ApiOperation("方法注释添加所有老师方法")
    public Object add(@ApiParam("用户")User user){
        return "Hello SpringBoot!";
    }

    @PutMapping("update")
    @ApiOperation("方法注释修改所有老师方法")
    public Object update(){
        return "Hello SpringBoot!";
    }

    @DeleteMapping("delete")
    @ApiOperation("方法注释删除所有老师方法")
    public Object delete(){
        return "Hello SpringBoot!";
    }

}

```

UserController和StudentController未展示



### 5.测试

1.访问地址

```http
http://localhost/swagger-ui.html

```

注意：这里我改了端口为80，所以不用显示输入端口



2.跳转到首页

![在这里插入图片描述](https://img-blog.csdnimg.cn/ecd8c7ffbe7547e3b3098b984de51aba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16)



3.查看TeacherController的信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/35139b4379454d35a592fbd06626b449.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16)



4.查看add方法

![在这里插入图片描述](https://img-blog.csdnimg.cn/3a9ec3ca4b5c408e80da130619eea221.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6Zey6KiAXw==,size_20,color_FFFFFF,t_70,g_se,x_16)



5.完结，主要的代码还是在Swagger配置，其他都是加注解就行了



## 13.任务

### 13.1异步任务

  异步处理还是非常常用的，比如我们在网站上发送邮件，后台会去发送邮件，此时前台会造成响应不动，直到邮件发送完毕，响应才会成功，所以我们一般会采用多线程的方式去处理这些任务。

  编写方法，假装正在处理数据，使用线程设置一些延时，模拟同步等待的情况；

`@EnableAsync` 开启异步注解功能
`@Async `告诉spring 这是一个`异步方法`

**启动类**

```java
@EnableAsync//开启异步注解功能
@SpringBootApplication
public class Demo6TestApplication {

    public static void main(String[] args) {
        SpringApplication.run(Demo6TestApplication.class, args);
    }

}

```



**service层**
  SpringBoot就会自己开一个线程池，进行调用！但是要让这个注解生效，还需要在主程序上添加一个注解`@EnableAsync` ，开启异步注解功能；

```java
@Service
public class AsyncService {

    //告诉spring 这是一个异步方法
    @Async
    public void hello(){
        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("数据正在处理");

    }
}

```



**controller层**

```java
@RestController
public class AsyncController {

    @Autowired
    private AsyncService asyncService;

    /**
     *  hello 请求
     * @return
     */
    @RequestMapping("/hello")
    public String hello(){
        asyncService.hello();//停止3秒
        return "OK";
    }
}

```



### 13.2邮件任务

邮件发送，在我们的日常开发中，也非常的多，Springboot也帮我们做了支持

1. 邮件发送需要引入`spring-boot-start-mail`
2. SpringBoot 自动配置`MailSenderAutoConfiguration`
3. 定义`MailProperties`内容，配置在`application.yml`中
4. 自动装配`JavaMailSender`
5. 测试邮件发送

**1.导入依赖**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>

```

看它引入的依赖，可以看到 jakarta.mail

![在这里插入图片描述](https://img-blog.csdnimg.cn/7d99d473ed7c40fe8692c78611d88df4.png#pic_center)



**2、查看自动配置类**：`MailSenderAutoConfiguration`

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass({ MimeMessage.class, MimeType.class, MailSender.class })
@ConditionalOnMissingBean(MailSender.class)
@Conditional(MailSenderCondition.class)
@EnableConfigurationProperties(MailProperties.class)
@Import({ MailSenderJndiConfiguration.class, MailSenderPropertiesConfiguration.class })
public class MailSenderAutoConfiguration {

   /**
    * Condition to trigger the creation of a {@link MailSender}. This kicks in if either
    * the host or jndi name property is set.
    */
   static class MailSenderCondition extends AnyNestedCondition {

      MailSenderCondition() {
         super(ConfigurationPhase.PARSE_CONFIGURATION);
      }

      @ConditionalOnProperty(prefix = "spring.mail", name = "host")
      static class HostProperty {

      }

      @ConditionalOnProperty(prefix = "spring.mail", name = "jndi-name")
      static class JndiNameProperty {

      }

   }

}

```



这个类没有注册bean，看它导入的bean

![在这里插入图片描述](https://img-blog.csdnimg.cn/3310a90e448c48f7be8f95de3ed9af6e.png#pic_center)

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass(Session.class)
@ConditionalOnProperty(prefix = "spring.mail", name = "jndi-name")
@ConditionalOnJndi
class MailSenderJndiConfiguration {

   private final MailProperties properties;

   MailSenderJndiConfiguration(MailProperties properties) {
      this.properties = properties;
   }

   @Bean
   JavaMailSenderImpl mailSender(Session session) {
      JavaMailSenderImpl sender = new JavaMailSenderImpl();
      sender.setDefaultEncoding(this.properties.getDefaultEncoding().name());
      sender.setSession(session);
      return sender;
   }

   @Bean
   @ConditionalOnMissingBean
   Session session() {
      String jndiName = this.properties.getJndiName();
      try {
         return JndiLocatorDelegate.createDefaultResourceRefLocator().lookup(jndiName, Session.class);
      }
      catch (NamingException ex) {
         throw new IllegalStateException(String.format("Unable to find Session in JNDI location %s", jndiName), ex);
      }
   }

}

```



**看下配置文件**

![在这里插入图片描述](https://img-blog.csdnimg.cn/c53646800cd74f28bde1abc068505214.png#pic_center)

```yaml
spring.mail.username=xxx
spring.mail.password=xxxx
spring.mail.host=smtp.qq.com
# 开启加密（qq独有）
spring.mail.properties.smtp.ssl.enable=true

```

获取授权码：在QQ邮箱中的设置->账户->开启pop3和smtp服务



**4.测试**

```java
package cn.bloghut;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.mail.SimpleMailMessage;
import org.springframework.mail.javamail.JavaMailSenderImpl;
import org.springframework.mail.javamail.MimeMessageHelper;

import javax.mail.internet.MimeMessage;
import java.io.File;

@SpringBootTest
class Demo6TestApplicationTests {

    @Autowired
    private JavaMailSenderImpl mailSender;

    /**
     * 简单的邮件发送
     */
    @Test
    void contextLoads() {
        SimpleMailMessage simpleMailMessage = new SimpleMailMessage();
        simpleMailMessage.setSubject("闲言你好呀~");
        simpleMailMessage.setText("今天天气真好");

        simpleMailMessage.setTo("1765736057@qq.com");
        simpleMailMessage.setFrom("1765736057@qq.com");
        mailSender.send(simpleMailMessage);
    }

    /**
     * 复杂邮件发送
     */
    @Test
    public void test2() throws Exception{
        MimeMessage mimeMessage = mailSender.createMimeMessage();
        //组装
        MimeMessageHelper helper = new MimeMessageHelper(mimeMessage,true);
        //正文
        helper.setSubject("闲言你好呀~plus");
        helper.setText("<p style='color:red'>你要加油啊！</p>");

        //附件
        helper.addAttachment("1.png",new File("I:/1.png"));
        helper.addAttachment("2.png",new File("I:/1.png"));

        helper.setTo("1765736057@qq.com");
        helper.setFrom("1765736057@qq.com");

         mailSender.send(mimeMessage);
    }

}

```



### 13.3定时任务

1. 某一些时候执行一些操作
2. 比如说半夜12点日志输出
3. 某一个商品折扣
4. 写一些抢东西的脚本
5. 比如需要在每天凌晨的时候，分析一次前一天的日志信息



**Spring为我们提供了异步执行任务调度的方式，提供了两个接口**

1. `TaskExecutor`接口 任务执行者
2. `TaskScheduler`接口 任务调度者



**两个注解：**

1. @`EnableScheduling` 开启定时功能的注解
2. @`Scheduled` 表示什么时候执行



**`cron` 表达式**

1、创建一个ScheduledService

```java
@Service
public class ScheduledService {

    //在一个特定的时间执行这个方法_Timer
    //cron表达式

    /**
     * 30 15 10 * * ? 每天10点15分30秒 执行一次
     *
     */
    //秒 分 时 日 月 周
    @Scheduled(cron = "0 * 22 * * ?")
    public void hello(){
        System.out.println("你被执行了"+new Date());
    }

}

```

2、这里写完定时任务之后，我们需要在启动类上增加@EnableScheduling 开启定时任务功能

```java
@EnableScheduling//开启定时任务
@EnableAsync//开启异步注解功能
@SpringBootApplication
public class Demo6TestApplication {

    public static void main(String[] args) {
        SpringApplication.run(Demo6TestApplication.class, args);
    }

}

```

**常用表达式**

```yaml
（1）0/2 * * * * ?   表示每2秒 执行任务
（1）0 0/2 * * * ?   表示每2分钟 执行任务
（1）0 0 2 1 * ?   表示在每月的1日的凌晨2点调整任务
（2）0 15 10 ? * MON-FRI   表示周一到周五每天上午10:15执行作业
（3）0 15 10 ? 6L 2002-2006   表示2002-2006年的每个月的最后一个星期五上午10:15执行作
（4）0 0 10,14,16 * * ?   每天上午10点，下午2点，4点
（5）0 0/30 9-17 * * ?   朝九晚五工作时间内每半小时
（6）0 0 12 ? * WED   表示每个星期三中午12点
（7）0 0 12 * * ?   每天中午12点触发
（8）0 15 10 ? * *   每天上午10:15触发
（9）0 15 10 * * ?     每天上午10:15触发
（10）0 15 10 * * ?   每天上午10:15触发
（11）0 15 10 * * ? 2005   2005年的每天上午10:15触发
（12）0 * 14 * * ?     在每天下午2点到下午2:59期间的每1分钟触发
（13）0 0/5 14 * * ?   在每天下午2点到下午2:55期间的每5分钟触发
（14）0 0/5 14,18 * * ?     在每天下午2点到2:55期间和下午6点到6:55期间的每5分钟触发
（15）0 0-5 14 * * ?   在每天下午2点到下午2:05期间的每1分钟触发
（16）0 10,44 14 ? 3 WED   每年三月的星期三的下午2:10和2:44触发
（17）0 15 10 ? * MON-FRI   周一至周五的上午10:15触发
（18）0 15 10 15 * ?   每月15日上午10:15触发
（19）0 15 10 L * ?   每月最后一日的上午10:15触发
（20）0 15 10 ? * 6L   每月的最后一个星期五上午10:15触发
（21）0 15 10 ? * 6L 2002-2005   2002年至2005年的每月的最后一个星期五上午10:15触发
（22）0 15 10 ? * 6#3   每月的第三个星期五上午10:15触发

```



**详细了解下`cron`表达式；**

```http
https://www.bejson.com/othertools/cron/

```



## 14.分布式

### 14.1什么是分布式系统？

在《分布式系统原理与范型》一书中有如下定义：“分布式系统是`若干独立计算机的集合`，这些计算机`对于用户来说就像单个相关系统`”；



![在这里插入图片描述](https://img-blog.csdnimg.cn/42281460f5d14d17ba7c4fd419876215.png#pic_center)



分布式系统是由一组`通过网络进行通信`、为了完成共同的任务而协调工作的计算机节点组成的系统。分布式系统的出现是为了用廉价的、普通的机器完成单个计算机无法完成的计算、存储任务。其目的是`利用更多的机器，处理更多的数据。`

分布式系统（distributed system）是`建立在网络`之上的软件系统。

  首先需要明确的是，只有当单个节点的处理能力无法满足日益增长的计算、存储任务的时候，且硬件的提升（加内存、加磁盘、使用更好的CPU）高昂到得不偿失的时候，应用程序也不能进一步优化的时候，我们才需要考虑分布式系统。因为，分布式系统要解决的问题本身就是和单机系统一样的，而由于分布式系统多节点、通过网络通信的拓扑结构，会引入很多单机系统没有的问题，为了解决这些问题又会引入更多的机制、协议，带来更多的问题。。。

**Dubbo文档**
随着互联网的发展，网站应用的规模不断扩大，常规的垂直应用架构已无法应对，分布式服务架构以及流动计算架构势在必行，`急需一个治理系统`确保架构有条不紊的演进。
在Dubbo的官网文档有这样一张图

![在这里插入图片描述](https://img-blog.csdnimg.cn/8719b9f7b1e54380a8f45f4e55269fe8.png#pic_center)



**单一应用架构**
  当网站流量很小时，只需一个应用，将所有功能都部署在一起，以减少部署节点和成本。此时，用于简化增删改查工作量的数据访问框架(ORM)是关键。

![在这里插入图片描述](https://img-blog.csdnimg.cn/3417134926f1454db540ade8029db126.png#pic_center)



适用于小型网站，小型管理系统，将所有功能都部署到一个功能里，简单易用。
**缺点：**
  1、性能扩展比较难
  2、协同开发问题
  3、不利于升级维护



**垂直应用架构**
  当访问量逐渐增大，单一应用增加机器带来的加速度越来越小，将应用拆成互不相干的几个应用，以提升效率。此时，用于加速前端页面开发的Web框架(MVC)是关键。

![在这里插入图片描述](https://img-blog.csdnimg.cn/86974fa31bb240a6aaa7026607faf66d.webp#pic_center)



通过切分业务来实现各个模块独立部署，降低了维护和部署的难度，团队各司其职更易管理，性能扩展也更方便，更有针对性。
**缺点：**`公用模块无法重复利用，开发性的浪费`



**分布式服务架构**
  当垂直应用越来越多，应用之间交互不可避免，`将核心业务抽取出来，作为独立的服务`，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求。此时，用于提高业务复用及整合的`分布式服务框架(RPC)`是关键。

![在这里插入图片描述](https://img-blog.csdnimg.cn/583eddc7a12f4638943e717091fd2049.png#pic_center)



**流动计算架构**
  当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于提高机器利用率的资源调度和治理中心(SOA)[ Service Oriented Architecture]是关键。

![在这里插入图片描述](https://img-blog.csdnimg.cn/019b736d39ef4654a2b554a54e4deb44.png#pic_center)



### 14.2什么是RPC?

`http`: 通信协议
`rpc`：通信协议

![在这里插入图片描述](https://img-blog.csdnimg.cn/c759968bec1941faaa8aba761564fb91.png#pic_center)



`RPC【Remote Procedure Call】是指远程过程调用，是一种进程间通信方式，他是一种技术的思想`，而不是规范。它允许程序调用另一个地址空间（通常是共享网络的另一台机器上）的过程或函数，而不用程序员显式编码这个远程调用的细节。即程序员无论是调用本地的还是远程的函数，本质上编写的调用代码基本相同。

  也就是说两台服务器A，B，一个应用部署在A服务器上，想要调用B服务器上应用提供的函数/方法，由于不在一个内存空间，不能直接调用，需要通过网络来表达调用的语义和传达调用的数据。为什么要用RPC呢？就是无法在一个进程内，甚至一个计算机内通过本地调用的方式完成的需求，比如不同的系统间的通讯，甚至不同的组织间的通讯，由于计算能力需要横向扩展，需要在多台机器组成的集群上部署应用。RPC就是要像调用本地的函数一样去调远程函数；



**RPC基本原理**

![在这里插入图片描述](https://img-blog.csdnimg.cn/26374699103c429d81d20e3b89016c2d.png#pic_center)



**步骤解析：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/0f5a5c2e1f9241e4a8dd075929eb1630.png#pic_center)



**RPC两个核心模块：通讯，序列化。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/85e3c61cfe584eabb4e75c680bb87c86.png#pic_center)



### 14.3如何给老婆解释什么是RPC

1. 一个阳光明媚的早晨，老婆又在翻看我订阅的技术杂志。
2. “老公，什么是RPC呀，为什么你们程序员那么多黑话！”，老婆还是一如既往的好奇。
3. “RPC，就是Remote Procedure Call的简称呀，翻译成中文就是远程过程调用嘛”，我一边看着书，一边漫不经心的回答着。
4. “啥？你在说啥？谁不知道翻译成中文是什么意思？你个废柴，快给我滚去洗碗！”
5. “我去。。。”，我如梦初醒，我对面坐着的可不是一个程序员，为了不去洗碗，我瞬间调动起全部脑细胞，星辰大海在我脑中汇聚，灵感涌现…
6. "是这样，远程过程调用，自然是相对于本地过程调用来说的嘛。
7. “嗯哼，那先给老娘讲讲，本地过程调用是啥子？”
8. “本地过程调用，就好比你现在在家里，你要想洗碗，那你直接把碗放进洗碗机，打开洗碗机开关就可以洗了。这就叫本地过程调用。”
9. “哎呦，我可不干，那啥是远程过程调用？”
10. “远程嘛，那就是你现在不在家，跟姐妹们浪去了，突然发现碗还没洗，打了个电话过来，叫我去洗碗，这就是远程过程调用啦”，多么通俗易懂的解释，我真是天才！
11. “哦！我明白了”，说着，老婆开始收拾包包。
12. “你这是干啥去哦”
13. “我？我要出门浪去呀，待会记得接收我的远程调用哦，哦不，咱们要专业点，应该说，待会记得接收我的RPC哦！



### 14.4什么是Dubbo

```
是一个Jar包
```

  Apache Dubbo 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。

```http
dubbo官网 http://dubbo.apache.org/zh-cn/index.html

```

1.了解Dubbo的特性
2.查看官方文档



**dubbo基本概念**

![在这里插入图片描述](https://img-blog.csdnimg.cn/6a5e27b9144d411b84bb2b00a6b43696.png#pic_center)



专业的事，交给专业的人来做~不靠谱！

  `服务提供者（Provider）`：暴露服务的服务提供方，服务提供者在启动时，向注册中心注册自己提供的服务。

  `服务消费者（Consumer）`：调用远程服务的服务消费方，服务消费者在启动时，向注册中心订阅自己所需的服务，服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。

  `注册中心（Registry）`：注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者

  `监控中心（Monitor）`：服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心



**调用关系说明**

1. 服务容器负责`启动`，`加载`，`运行`服务提供者。
2. 服务`提供者`在启动时，`向注册中心注册自己提供的服务`。
3. 服务`消费者`在启动时，`向注册中心订阅自己所需的服务`。
4. 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。
5. 服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。
6. 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心。



### 14.5什么是zookeeper

**产生背景**

当今是个分布式、集群、云计算等名词满天飞的时代。造成这种局面的一个重要因素就是，单一机器的处理能力已经不能满足我们的需求，不得不采用由多台机器组成的服务集群。服务集群对外提供服务的过程中，可以分解处理压力，在一定程度上打破性能瓶颈，并提高服务的可用性（不会因为一台机器宕机而造成服务不可用）。

![在这里插入图片描述](https://img-blog.csdnimg.cn/f0f018edb6e94f9795ff9538509d6c53.png#pic_center)

上图中有三台机器，每台机器跑同样的一个应用程序。然后我们将这三台机器通过网络将其连接起来，构成一个系统来为用户提供服务，对用户来说这个系统的架构是透明的，他感觉不到这个系统是一个什么样的架构。那么我们就可以把这种系统称作一个分布式系统。

**那么，问题来了**：
  1.程序的运行往往依赖很多配置文件，比如数据库地址、黑名单控制、服务地址列表等，而且有些配置信息需要频繁地进行动态变更，这时候怎么保证所有机器共享的配置信息保持一致？

  2.如果有一台机器挂掉了，其他机器如何感知到这一变化并接管任务？如果用户激增，需要增加机器来缓解压力，如何做到不重启集群而完成机器的添加？

  3.用户数量增加或者减少，会出现有的机器资源使用率繁忙，有的却空闲，如何让每台机器感知到其他机器的负载状态从而实现负载均衡？

  4.在一台机器上要多个进程或者多个线程操作同一资源比较简单，因为可以有大量的状态信息或者日志信息提供保证，比如两个A和B进程同时写一个文件，加锁就可以实现。但是分布式系统怎么办？需要一个三方的分配锁的机制，几百台worker都对同一个网络中的文件写操作，怎么协同？还有怎么保证高效的运行？


除了上面列举的几种，还有很多细思极恐的问题，分布式系统到底有多然人抓狂，可以想想你第一次接触多线程的感觉;

**计划中的多线程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/8a218e27ec914173b28c42732e3f2ed3.png#pic_center)

**现实中的多线程**

![在这里插入图片描述](https://img-blog.csdnimg.cn/dabf61f2909544c484cd725d9a6a8009.png#pic_center)



分布式系统可以看作多线程的N级加强版……



ZooKeeper的前世今生
  分布式系统的很多难题，都是由于缺少协调机制造成的。
  目前，在分布式协调技术方面做得比较好的就是Google的Chubby还有Apache的ZooKeeper。有人会问既然有了Chubby为什么还要弄一个ZooKeeper，难道Chubby做得不够好吗？主要是Chubby是非开源的，Google自家用。后来`雅虎模仿Chubby开发出了ZooKeeper`，也实现了类似的分布式锁的功能，并且将ZooKeeper作为一种开源的程序捐献给了Apache，那么这样就可以使用ZooKeeper所提供锁服务。而且在分布式领域久经考验，它的可靠性，可用性都是经过理论和实践的验证的。
![在这里插入图片描述](https://img-blog.csdnimg.cn/61714940478b47ffab7fc46faf99ccdd.png#pic_center)

至于这个神器为什么叫ZooKeeper，与外国人一贯的幽默精神有关。
  众所周知，外国人喜欢给用一个动物作为吉祥物，在IT界也不例外。比如，负责大数据工作的Hadoop是一个黄色的大象；负责数据仓库的Hive是一个虚拟蜂巢；负责数据分析的Apache Pig是一头聪明的猪；负责管理web容器的tomcat是一只雄猫……那好，负责分布式协调工作的角色就叫ZooKeeper（动物园饲养员）吧。



ZooKeeper能干什么
官方说辞是：
  ZooKeeper 分布式服务框架是Apache Hadoop 的一个子项目，它`主要是用来解决分布式应用中经常遇到的一些数据管理问题`，如：统一命名服务、状态同步服务、集群管理、分布式应用配置项的管理等。简化分布式应用协调及其管理的难度，提供高性能的分布式服务。ZooKeeper的目标就是封装好复杂 易出错的关键服务，将简单易用的接口和性能高效、功能稳定的系统提供给用户。
ZooKeeper在一致性、可用性、容错性的保证，也是ZooKeeper的成功之处，它获得的一切成功都与它采用的协议——Zab协议是密不可分的。

  为了实现前面提到的各种服务，比如分布式锁、配置维护、组服务等，ZooKeeper设计了一种新的数据结构——Znode，然后在该数据结构的基础上定义了一些原语，也就是一些关于该数据结构的一些操作。有了这些数据结构和原语还不够，因为ZooKeeper工作在分布式环境下，服务是通过消息以网络的形式发送给分布式应用程序，所以还需要一个通知机制——Watcher机制。总结一下，ZooKeeper所提供的服务主要是通过：数据结构 + 原语 + watcher机制，三个部分来实现的。




### 14.6安装dubbo-admin

`是一个监控管理后台~查看我们注册了哪些服务，哪些服务被消费了`

dubbo本身并不是一个服务软件。`它其实就是一个jar包`，能够帮你的java程序连接到zookeeper，并利用zookeeper消费、提供服务。

  但是为了让用户更好的管理监控众多的dubbo服务，官方提供了一个可视化的监控程序dubbo-admin，不过这个监控即使不装也不影响使用。
这里来安装一下：

**下载dubbo-admin**

```http
地址 ：https://github.com/apache/dubbo-admin/tree/master

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/c6ea3d5fa0f44def9e307ead00b64ffe.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/c29c3003fd1347b294153ec2949aa720.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/d352ab60e5e047bf8c51e65cccd1ee9f.png#pic_center)



**解压进入目录**
修改 dubbo-admin\src\main\resources \application.properties 指定zookeeper地址

![在这里插入图片描述](https://img-blog.csdnimg.cn/a76a4fcf1fc84fdcab889afbca6df2c9.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/6b85b20d389447acb478798c85f42b3c.png#pic_center)

**在项目目录下打包dubbo-admin**
清除并打包

```yaml
mvn clean package -Dmaven.test.skip=true

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/564c8303ea7e48299c10cc00285a9a54.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/6bb017dd4ec944148629a91b92ed0829.png#pic_center)

打包完成

![在这里插入图片描述](https://img-blog.csdnimg.cn/e4de35601b984799b0bc99ae9f6d1258.png#pic_center)

启动jar 包

![在这里插入图片描述](https://img-blog.csdnimg.cn/12ae916f373b4007a12c8ab054badfa8.png#pic_center)

记得启动zookeeper

![在这里插入图片描述](https://img-blog.csdnimg.cn/56316bdd3c7e44978fe69dce134e1050.png#pic_center)

**访问**

```http
http://localhost:7001/

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/21d7ead0d6e64686956f5cff992d8f8b.png#pic_center)



用户名和密码都是root

![在这里插入图片描述](https://img-blog.csdnimg.cn/474455727db74c14a03519144e398171.png#pic_center)







## 15.SpringSecurity

在web开发中，安全第一位！过滤器，拦截器。。。

功能性需求：否

做网站：安全应该在什么时候考虑？

- 漏洞，隐私泄露~
- 架构一旦确定~



shiro、SpringSecurity:很像~除了类不一样，名字不一样；

认证，授权（vip1,vip2,vip3）



- 功能权限
- 访问权限
- 菜单权限
- ...拦截器，过滤器：大量原生代码~冗余



MVC-->Spring-->SpringBoot--->框架思想



### 简介

Spring Security 是针对Spring项目的安全框架，也是Spring Boot底层安全模块默认的技术选型，他可以实现强大的Web安全控制，对于安全控制，我们仅需要引入 spring-boot-starter-security 模块，进行少量的配置，即可实现强大的安全管理！



- 几个重要的类：
  WebSecurityConfigurerAdapter：自定义Security策略
  AuthenticationManagerBuilder：自定义认证策略
- @EnableWebSecurity：开启WebSecurity模式



Spring Security的两个主要目标是 “认证” 和 “授权”（访问控制）。

- **“认证”（Authentication）**
  身份验证是关于验证您的凭据，如用户名/用户ID和密码，以验证您的身份。
  身份验证通常通过用户名和密码完成，有时与身份验证因素结合使用。
- **“授权” （Authorization）**
  授权发生在系统成功验证您的身份后，最终会授予您访问资源（如信息，文件，数据库，资金，位置，几乎任何内容）的完全权限。

这个概念是通用的，而不是只在Spring Security 中存在。



### 3、认证和授权

#### 3.1 引入 Spring Security 模块

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

```



#### 3.2 编写 Spring Security 配置类

```java
@EnableWebSecurity//开启WebSecurity模式
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    //授权
    @Override
    protected void configure(HttpSecurity http) throws Exception {

        //首页所有用户可以访问，功能页只有对应有权限的人才能访问
        http.authorizeRequests()
                .antMatchers("/").permitAll()
                .antMatchers("/level1/**").hasRole("vip1")
                .antMatchers("/level2/**").hasRole("vip2")
                .antMatchers("/level3/**").hasRole("vip3");

        //设置没有权限访问会跳转到登录页
        http.formLogin();
    }

    //认证
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        //防止反编译，对明文密码进行编译：BCryptPasswordEncoder()
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                .withUser("sgx").password(new BCryptPasswordEncoder().encode("123")).roles("vip2","vip3")
                .and()
                .withUser("root").password(new BCryptPasswordEncoder().encode("456")).roles("vip1","vip2","vip3")
                .and()
                .withUser("admin").password(new BCryptPasswordEncoder().encode("789")).roles("vip1","vip3");
    }
}

```



**正常业务中：从数据库中读取用户名和密码**

![在这里插入图片描述](https://img-blog.csdnimg.cn/2264b6c3b5f14b9db41129449f397b91.png)



注意点：

- 在授权中设置每个角色可以访问的页面，同时设置跳转登录页
- 在认证中设置用户角色；
- Spring security 5.0中新增了多种加密方式，也改变了密码的格式。要想我们的项目还能够正常登陆，需要修改一下configure中的代码。我们要将前端传过来的密码进行某种方式加密，spring security 官方推荐的是使用bcrypt加密方式。



#### 3.3 测试

每个用户只能访问对应权限的页面



### 4、权限控制和注销

#### 4.1注销登录

##### 4.1.1 开启自动配置的注销功能，

注销后默认跳转到登录页，可以设置注销成功后跳转到首页

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
.....
    //注销登录,跳回首页(默认会返回到登录页）
    http.logout().logoutSuccessUrl("/");
}

```



##### 4.1.2 在前端页面添加一个注销按钮

```html
<a class="item" th:href="@{/logout}">
    <i class="address card icon"></i> 注销
</a>

```



#### 4.1.3 测试

### 4.2 权限控制

- 要求1：未登录，只显示登录按钮；登录后，显示用户名，用户权限和注销按钮；
- 要求2：登录成功后，用户只能看到自己权限内的模块；

##### 4.2.1 导入thymeleaf和springSecurity整合包

```xml
<!--springSecurity和thymeleaf整合包-->
<dependency>
    <groupId>org.thymeleaf.extras</groupId>
    <artifactId>thymeleaf-extras-springsecurity4</artifactId>
    <version>3.0.4.RELEASE</version>
</dependency>

```



##### 4.2.2 降低springboot版本，此功能最高支持到2.0.9

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.9.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

```



##### 4.2.3 前端页面导入命名空间，修改前端页面实现要求1

```xml
xmlns:sec="http://www.thymeleaf.org/thymeleaf-extras-springsecurity4">

```

```html
<!--如果未登录，显示登录-->
<div sec:authorize="!isAuthenticated()">
    <a class="item" th:href="@{/toLogin}">
        <i class="address card icon"></i> 登录
    </a>
</div>

<!--如果已登录，显示注销-->
<div sec:authorize="isAuthenticated()">
    <a class="item" >
       用户名：<span sec:authentication="name"></span>
权限：<span sec:authentication="principal.authorities"></span>
    </a>
</div>
<div sec:authorize="isAuthenticated()">
    <a class="item" th:href="@{/logout}">
        <i class="address card icon"></i> 注销
    </a>
</div>

```



##### 4.2.4 修改前端页面实现要求B

```html
<div class="column" sec:authorize="hasRole('vip1')">
<div class="column" sec:authorize="hasRole('vip2')">
<div class="column" sec:authorize="hasRole('vip3')">

```



![在这里插入图片描述](https://img-blog.csdnimg.cn/00f57f34fe3e4d0b927c4b0f4a574fba.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/690c0a517abf4ba68981724f35597738.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/35bb88cdc67249e4b08250263a68dcf4.png)



- 注意：如果点击注销后提示404，是**因为它默认防止csrf跨站请求伪造**，因为会产生安全问题，我们可以将请求改为post表单提交，或者在spring security中关闭csrf功能；

```java
//关闭csrf防止网站攻击
http.csrf().disable();

```



### 5、首页定制和记住我功能

#### 5.1 首页定制：指定登录页

```java
//设置没有权限访问会跳转到登录页
http.formLogin().loginPage("/toLogin");

```

注意1：当前端表单提交的路径为login，后端需要指定真正权限认定的路由

```html
<form th:action="@{/login}" method="post">

```

```java
http.formLogin().loginPage("/toLogin").loginProcessingUrl("login");

```



注意2：当前端表单提交的参数名和后端默认接收的参数名不一致，可以指定接收

```html
<input type="text" placeholder="Username" name="user">
<input type="password" name="pwd">

```

```java
http.formLogin().loginPage("/toLogin").usernameParameter("user").passwordParameter("pwd").loginProcessingUrl("/login");

```



#### 5.2 记住我

```java
//开启记住我功能，指定接收的参数名
http.rememberMe().rememberMeParameter("remember");

```



- 前端页面：

```html
<input type="checkbox" name="remember" /> 记住我

```



**总结：完整的SpringSecurity配置代码**

```java
@EnableWebSecurity//开启WebSecurity模式
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    //授权
    @Override
    protected void configure(HttpSecurity http) throws Exception {

        //首页所有用户可以访问，功能页只有对应有权限的人才能访问
        http.authorizeRequests()
                .antMatchers("/").permitAll()
                .antMatchers("/level1/**").hasRole("vip1")
                .antMatchers("/level2/**").hasRole("vip2")
                .antMatchers("/level3/**").hasRole("vip3");

        //设置没有权限访问会跳转到登录页
        http.formLogin().loginPage("/toLogin")
                .usernameParameter("user")
                .passwordParameter("pwd")
                .loginProcessingUrl("/login");
        
        //关闭csrf防止网站攻击
        http.csrf().disable();

        //注销登录,跳回首页(默认会返回到登录页）
        http.logout().logoutSuccessUrl("/");

        //开启记住我功能
        http.rememberMe().rememberMeParameter("remember");

    }

    //认证
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        //防止反编译，对明文密码进行编译：BCryptPasswordEncoder()
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
                .withUser("sgx")
                .password(new BCryptPasswordEncoder().encode("123"))
                .roles("vip2","vip3")
                .and()
                .withUser("root")
                .password(new BCryptPasswordEncoder().encode("456"))
                .roles("vip1","vip2","vip3")
                .and()
                .withUser("admin")
                .password(new BCryptPasswordEncoder().encode("789"))
                .roles("vip1");
    }
}

```



## 16.Shiro

### 1. 简介

**[Apache](https://so.csdn.net/so/search?q=Apache&spm=1001.2101.3001.7020)** Shiro是一个强大且易用的Java安全框架

可以完成身份验证、授权、密码和会话管理

[**Shiro**](https://so.csdn.net/so/search?q=Shiro&spm=1001.2101.3001.7020) 不仅可以用在 JavaSE 环境中，也可以用在 JavaEE 环境中

官网： http://shiro.apache.org/



### 2. 功能

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020092014264672.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



`Authentication`：身份认证/登录，验证用户是不是拥有相应的身份；

`Authorization`：授权，即权限验证，验证某个已认证的用户是否拥有某个权限；即判断用户是否能做事情，常见的如：验证某个用户是否拥有某个角色。或者细粒度的验证某个用户对某个资源是否具有某个权限；

`Session Manager`：会话管理，即用户登录后就是一次会话，在没有退出之前，它的所有信息都在会话中；会话可以是普通JavaSE环境的，也可以是如Web环境的；

`Cryptography`：加密，保护数据的安全性，如密码加密存储到数据库，而不是明文存储；

`Web Support`：Web支持，可以非常容易的集成到Web环境；

`Caching`：缓存，比如用户登录后，其用户信息、拥有的角色/权限不必每次去查，这样可以提高效率；

`Concurrency`：shiro支持多线程应用的并发验证，即如在一个线程中开启另一个线程，能把权限自动传播过去；

`Testing`：提供测试支持；

`Run As`：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问；

`Remember Me`：记住我，这个是非常常见的功能，即一次登录后，下次再来的话不用登录了。



### 3. 从外部看

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920142859228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



应用代码直接交互的对象是Subject，也就是说Shiro的对外API核心就是Subject；其每个API的含义：

`Subject`：主体，代表了当前“用户”，这个用户不一定是一个具体的人，与当前应用交互的任何东西都是Subject，如网络爬虫，机器人等；即一个抽象概念；所有Subject都绑定到SecurityManager，与Subject的所有交互都会委托给SecurityManager；可以把Subject认为是一个门面；SecurityManager才是实际的执行者；

`SecurityManager`：安全管理器；即所有与安全有关的操作都会与SecurityManager交互；且它管理着所有Subject；可以看出它是Shiro的核心，它负责与后边介绍的其他组件进行交互，如果学习过SpringMVC，你可以把它看成DispatcherServlet前端控制器；

`Realm`：域，Shiro从从Realm获取安全数据（如用户、角色、权限），就是说SecurityManager要验证用户身份，那么它需要从Realm获取相应的用户进行比较以确定用户身份是否合法；也需要从Realm得到用户相应的角色/权限进行验证用户是否能进行操作；可以把Realm看成DataSource，即安全数据源。

也就是说对于我们而言，最简单的一个Shiro应用：

1. 应用代码通过Subject来进行认证和授权，而Subject又委托给SecurityManager；

2. 我们需要给Shiro的SecurityManager注入Realm，从而让SecurityManager能得到合法的用户及其权限进行判断。


从以上也可以看出，Shiro不提供维护用户/权限，而是通过Realm让开发人员自己注入



### 4. 外部架构

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920143302296.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



`Subject`：主体，可以看到主体可以是任何可以与应用交互的“用户”；

`SecurityManager`：相当于SpringMVC中的DispatcherServlet或者Struts2中的FilterDispatcher；是Shiro的心脏；所有具体的交互都通过SecurityManager进行控制；它管理着所有Subject、且负责进行认证和授权、及会话、缓存的管理。

`Authenticator`：认证器，负责主体认证的，这是一个扩展点，如果用户觉得Shiro默认的不好，可以自定义实现；其需要认证策略（Authentication Strategy），即什么情况下算用户认证通过了；

`Authrizer`：授权器，或者访问控制器，用来决定主体是否有权限进行相应的操作；即控制着用户能访问应用中的哪些功能；

`Realm`：可以有1个或多个Realm，可以认为是安全实体数据源，即用于获取安全实体的；可以是JDBC实现，也可以是LDAP实现，或者内存实现等等；由用户提供；注意：Shiro不知道你的用户/权限存储在哪及以何种格式存储；所以我们一般在应用中都需要实现自己的Realm；

`SessionManager`：如果写过Servlet就应该知道Session的概念，Session呢需要有人去管理它的生命周期，这个组件就是SessionManager；而Shiro并不仅仅可以用在Web环境，也可以用在如普通的JavaSE环境、EJB等环境；所有呢，Shiro就抽象了一个自己的Session来管理主体与应用之间交互的数据；这样的话，比如我们在Web环境用，刚开始是一台Web服务器；接着又上了台EJB服务器；这时想把两台服务器的会话数据放到一个地方，这个时候就可以实现自己的分布式会话（如把数据放到Memcached服务器）；

`SessionDAO`：DAO大家都用过，数据访问对象，用于会话的CRUD，比如我们想把Session保存到数据库，那么可以实现自己的SessionDAO，通过如JDBC写到数据库；比如想把Session放到Memcached中，可以实现自己的Memcached SessionDAO；另外SessionDAO中可以使用Cache进行缓存，以提高性能；

`CacheManager`：缓存控制器，来管理如用户、角色、权限等的缓存的；因为这些数据基本上很少去改变，放到缓存中后可以提高访问的性能

`Cryptography`：密码模块，Shiro提高了一些常见的加密组件用于如密码加密/解密的



### 5. 认证流程

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200923201850784.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



**用户** 提交 **身份信息、凭证信息** 封装成 **令牌** 交由 **安全管理器** 认证



### 2. 快速入门

#### 1. 拷贝案例

1.按照官网提示找到 快速入门案例

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920145233350.png#pic_center)



GitHub地址：[shiro/samples/quickstart/](https://github.com/apache/shiro/tree/master/samples/quickstart)

从GitHub 的文件中可以看出这个快速入门案例是一个 Maven 项目

2.新建一个 Maven 工程，删除其 src 目录，将其作为父工程

3.在父工程中新建一个 Maven 模块

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920145529257.png#pic_center)

4.复制快速入门案例 POM.xml 文件中的依赖 （版本号自选）

```xml
<dependencies>
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
            <version>1.4.1</version>
        </dependency>

        <!-- configure logging -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>1.7.29</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.29</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
    </dependencies>

```



5.把快速入门案例中的 resource 下的`log4j.properties` 复制下来

6.复制一下 `shiro.ini` 文件

7.复制一下 `Quickstart.java` 文件
如果有导包的错误，把那两个错误的包删掉，就会自动导对的包了，快速入门案例中用的方法过时了

8.运行 `Quickstart.java`，得到结果

![在这里插入图片描述](https://img-blog.csdnimg.cn/2020092015184736.png#pic_center)



#### 2. 分析案例

1.通过 SecurityUtils 获取当前执行的用户 Subject

```java
Subject currentUser = SecurityUtils.getSubject();

```

2.通过 当前用户拿到 Session

```java
Session session = currentUser.getSession();

```

3.用 Session 存值取值

```java
session.setAttribute("someKey", "aValue");
        String value = (String) session.getAttribute("someKey");

```

4.判断用户是否被认证

```java
currentUser.isAuthenticated()

```

5.执行登录操作

```java
 currentUser.login(token);

```

6.打印其标识主体

```java
currentUser.getPrincipal()

```

7.注销

```java
currentUser.logout();

```

8.总览

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920155324660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



### 3. SpringBoot 集成 Shiro

#### 1. 编写配置文件

1. 在刚刚的父项目中新建一个 springboot 模块
2. 导入 SpringBoot 和 Shiro 整合包的依赖

```xml
<!--SpringBoot 和 Shiro 整合包-->
		<!-- https://mvnrepository.com/artifact/org.apache.shiro/shiro-spring-boot-web-starter -->
		<dependency>
			<groupId>org.apache.shiro</groupId>
			<artifactId>shiro-spring-boot-web-starter</artifactId>
			<version>1.6.0</version>
		</dependency>

```



- 下面是编写配置文件

  Shiro 三大要素

- subject -> ShiroFilterFactoryBean
- securityManager -> DefaultWebSecurityManager
- realm

实际操作中对象创建的顺序 ： realm -> securityManager -> subject



3.编写自定义的 realm ，需要继承 `AuthorizingRealm`

```java
//自定义的 Realm
public class UserRealm extends AuthorizingRealm {
    //授权

    @Override
    protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
        //打印一个提示
        System.out.println("执行了授权方法");
        return null;
    }

    //认证

    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
        //打印一个提示
        System.out.println("执行了认证方法");
        return null;
    }
}

```



4.新建一个 `ShiroConfig`配置文件
1、按照上面说的创建过程来写
创建 `Realm`

```java
//3. realm
    //让 spring 托管自定义的 realm 类
    @Bean
    public UserRealm userRealm(){
        return new UserRealm();
    }

```

2、创建 `securityManager`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920163757569.png#pic_center)



需要传入一个 Realm

```java
//2. securityManager -> DefaultWebSecurityManager
    // @Qualifier("userRealm") 指定 Bean 的名字为 userRealm
    // spring 默认的 BeanName 就是方法名
    // name 属性 指定 BeanName
    @Bean(name = "SecurityManager")
    public DefaultWebSecurityManager getDefaultWebSecurity(@Qualifier("userRealm") UserRealm userRealm){
        DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
        //需要关联自定义的 Realm，通过参数把 Realm 对象传递过来
        securityManager.setRealm(userRealm);
        return securityManager;
    }

```



3、创建 `subject`

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200920163928569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDQ0OTgzOA==,size_16,color_FFFFFF,t_70#pic_center)



需要传入一个 securityManager

```java
//1. subject -> ShiroFilterFactoryBean
// @Qualifier("securityManager") 指定 Bean 的名字为 securityManager

@Bean(name = "shiroFilterFactoryBean")
public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("SecurityManager") DefaultWebSecurityManager securityManager){
    ShiroFilterFactoryBean subject = new ShiroFilterFactoryBean();
    //设置安全管理器
    //需要关联 securityManager ，通过参数把 securityManager 对象传递过来
    subject.setSecurityManager(securityManager);
    return subject;
}


```



#### 2. 搭建简单测试环境

1. 新建一个登录页面
2. 新建一个首页
   首页上有三个链接，一个登录，一个增加用户，一个删除用户
3. 新建一个增加用户页面
4. 新建一个删除用户页面
5. 编写对应的 Controller



#### 3. 使用

**1. 登录拦截**

在上面的 `getShiroFilterFactoryBean` 方法中加上需要拦截的登录请求

```java
   @Bean(name = "shiroFilterFactoryBean")
    public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("SecurityManager") DefaultWebSecurityManager securityManager){
        ShiroFilterFactoryBean subject = new ShiroFilterFactoryBean();
        subject.setSecurityManager(securityManager);

//添加 Shiro 的内置过滤器=======================
        /*
            anon : 无需认证，就可以访问
            authc : 必须认证，才能访问
            user : 必须拥有 “记住我”功能才能用
            perms : 拥有对某个资源的权限才能访问
            role : 拥有某个角色权限才能访问
         */
        Map<String, String> map = new LinkedHashMap<>();
        // 设置 /user/addUser 这个请求,只有认证过才能访问
//        map.put("/user/addUser","authc");
//        map.put("/user/deleteUser","authc");
        // 设置 /user/ 下面的所有请求,只有认证过才能访问
        map.put("/user/*","authc");
        subject.setFilterChainDefinitionMap(map);
        // 设置登录的请求
        subject.setLoginUrl("/tologin");
//============================================
        return subject;
    }

```



测试
点击 addUser 链接，不会跳到 addUser 页面，而是跳到登录页，拦截成功



**2. 用户认证**

1. 在 Controller 中写一个登录的控制器

```java
//登录的方法
    @RequestMapping("/login")
    public String login(String username, String password, Model model) {
        //获取当前用户
        Subject subject = SecurityUtils.getSubject();
        //没有认证过
        //封装用户的登录数据,获得令牌
        UsernamePasswordToken token = new UsernamePasswordToken(username, password);

        //登录 及 异常处理
        try {
            //用户登录
            subject.login(token);
            return "index";
        } catch (UnknownAccountException uae) {
            //如果用户名不存在
            System.out.println("用户名不存在");
            model.addAttribute("exception", "用户名不存在");
            return "login";
        } catch (IncorrectCredentialsException ice) {
            //如果密码错误
            System.out.println("密码错误");
            model.addAttribute("exception", "密码错误");
            return "login";
        }
    }

```



2.重启，测试

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200921141625471.png#pic_center)



成功

**并且可以看出，是先执行了 自定义的 `UserRealm` 中的 `AuthenticationInfo` 方法，再执行了，登录的相关操作**

下面去自定义的 `UserRealm` 中的 `AuthenticationInfo` 方法中去获取用户信息



3.修改 `UserRealm` 中的 `AuthenticationInfo`

```java
@Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
        //打印一个提示
        System.out.println("执行了认证方法");

        // 用户名密码(暂时先自定义一个做测试)
        String name = "root";
        String password = "1234";

        //通过参数获取登录的控制器中生成的 令牌
        UsernamePasswordToken token = (UsernamePasswordToken) authenticationToken;
        //用户名认证
        if (!token.getUsername().equals(name)){
            // return null 就表示控制器中抛出的相关异常
            return null;
        }
        //密码认证， Shiro 自己做，为了避免和密码的接触
        //最后返回一个 AuthenticationInfo 接口的实现类，这里选择 SimpleAuthenticationInfo
        // 三个参数：获取当前用户的认证 ； 密码 ； 认证名
        return new SimpleAuthenticationInfo(principal, user.getPwd(), this.getName());
    }

```



4.测试
输入错误的密码

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200921143424629.png#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200921143435641.png#pic_center)

输入正确的密码
登录成功，且可以访问 那两个页面



#### 3. 退出登录

1. 在控制器中添加一个退出登录的方法

```java
//退出登录

@RequestMapping("/logout")
public String logout(){
    Subject subject = SecurityUtils.getSubject();
    subject.logout();
    return "login";
}

```

2.测试
   登出成功
