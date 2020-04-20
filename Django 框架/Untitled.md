```javascript
<script>
    $('#i1').click(function() {
        $.ajax({
            url:'host/',
            type:'POST',
            data:{'k1':'value'},
            success: function(data) {
                location.reload('indel.html')
            }
        })
    })
</script>
```





1、django有哪些插件

2、mtv，mcv有什么区别





我前两份的工作主要做的是系统运维，可以熟练得进行linux系统的维护与优化，也可以熟练安装部署和维护linux常用服务，es集群，redis集群，rabbitmq集群，mysql主从和mgr集群，像常用的监控软件，如zabbix，cacti，prometheus，grafana也可以熟练得安装维护和使用

第三份工作是运维开发：

1、运维平台CMDB模块开发，包含资产的初始化，内容包含监控的添加，系统参数优化，filebeat安装，配置信息管理，主机名，IP地址列表维护，机房地址，可以动态维护cpu，内存，硬盘等服务器硬件信息，所属环境， 账号密码管理，主机root密码过期维护，业务线模块管理，可以配置模块的日志路径，部署的服务器IP地址，开发负责人，运维负责人。不需要手动去维护，减少人工维护成本。

2、进程监控模块开发，通过服务器驻留程序获取进程的信息，通过监控模块的一系列计算，聚合，来判断进程是否down掉，完善了监控体系，减少了因为进程死掉引起故障的时间

3、日志收集模块开发，通过CMDB模块中业务线模块的信息和进程监控模块作关联，自动生成filebeat和logstash配置文件并更新，把日志按照业务线和模块进行分类，k8s的日志也会按照业务线和模块进行分类，nginx也会按照域名分到各自的业务线上，收集中用到的filebeat，logstash的配置文件都是自动生成与更新的，集成日志的查询，日志查询集成各种规则，实时日志的查询。 

4、日志监控模块，可以通过在页面配置日志报警规则，监控异常日志，报警的规则支持与或非，大于小于，复杂的查询规则。还有通过反射的机制来维护定制化的监控，使定位故障的速度得到提高。

5、Prometheus服务动态监控模块开发，通过服务的自动发现，自动为第  三方中间件添加监控，Mysql、Redis、RabbitMq、Kafka、Elasticsearch支持多进程进行监控， 有一些插件是自己写的为了监控阿里云的rds，redis，es，6、报警模块，钉钉+电话报警 报警统一接收并保存，也做了一些简单的收敛，网络的关联收敛，同类型的收敛， 默认发钉钉，当持续一段时间没恢复就电话报警 减少了许多没用的报警

7、运维平台发布模块开发，通过CMDB模块和Jenkins关联，通过运维平台进行发布，通过jenkins把镜像打包好，k8s发布模块中配置连接检测，根据配置模板进行对yml进行渲染，蓝绿发布，灰度发布中来完成发布流程的提交和程序的发布。

ingress-nginx实现灰度发布  

其他的还有些监控脚本开发，资产初始化脚本，ansible执行动态加载密码和其他一些属性，账单数据爬取工作

- etcd 
  用于持久化存储集群中所有的资源对象，如Node、Service、Pod、RC、Namespace等；API Server提供了操作etcd的封装接口API，这些API基本上都是集群中资源对象的增删改查及监听资源变化的接口。
- API Server 
  提供了资源对象的唯一操作入口，其他所有组件都必须通过它提供的API来操作资源数据，通过对相关的资源数据“全量查询”+“变化监听”，这些组件可以很“实时”地完成相关的业务功能。
- Controller Manager 
  集群内部的管理控制中心，其主要目的是实现Kubernetes集群的故障检测和恢复的自动化工作，比如根据RC的定义完成Pod的复制或移除，以确保Pod实例数符合RC副本的定义；根据Service与Pod的管理关系，完成服务的Endpoints对象的创建和更新；其他诸如Node的发现、管理和状态监控、死亡容器所占磁盘空间及本地缓存的镜像文件的清理等工作也是由Controller Manager完成的。
- Scheduler 
  集群中的调度器，负责Pod在集群节点中的调度分配。
- Kubelet 
  负责本Node节点上的Pod的创建、修改、监控、删除等全生命周期管理，同时Kubelet定时“上报”本Node的状态信息到API Server里。
- Proxy 
  实现了Service的代理与软件模式的负载均衡器。







- etcd 
  用于持久化存储集群中所有的资源对象，如Node、Service、Pod、RC、Namespace等；API Server提供了操作etcd的封装接口API，这些API基本上都是集群中资源对象的增删改查及监听资源变化的接口。
- API Server 
  提供了资源对象的唯一操作入口，其他所有组件都必须通过它提供的API来操作资源数据，通过对相关的资源数据“全量查询”+“变化监听”，这些组件可以很“实时”地完成相关的业务功能。
- Controller Manager 
  集群内部的管理控制中心，其主要目的是实现Kubernetes集群的故障检测和恢复的自动化工作，比如根据RC的定义完成Pod的复制或移除，以确保Pod实例数符合RC副本的定义；根据Service与Pod的管理关系，完成服务的Endpoints对象的创建和更新；其他诸如Node的发现、管理和状态监控、死亡容器所占磁盘空间及本地缓存的镜像文件的清理等工作也是由Controller Manager完成的。
- Scheduler 
  集群中的调度器，负责Pod在集群节点中的调度分配。
- Kubelet 
  负责本Node节点上的Pod的创建、修改、监控、删除等全生命周期管理，同时Kubelet定时“上报”本Node的状态信息到API Server里。
- Proxy 
  实现了Service的代理与软件模式的负载均衡器。