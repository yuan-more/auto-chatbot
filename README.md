# chatgpt 聊天机器人

## 项目介绍

本项目是一个基于DDD(COLA)架构的聊天机器人，解耦业务逻辑与外部接口。并且使用了【策略模式】来为后续增加**支持平台**和**其他回答模型**提供拓展点。

代码运行演示：

![代码演示](doc/%E4%BB%A3%E7%A0%81%E6%BC%94%E7%A4%BA.png)

## 一键启动

1. 修改`start`模块下的`application.yml`，或者通过**环境变量**的方式不用把密码硬编码在配置中
   * 获取open-ai的apikey(OPENAI_API_KEY)
   
   ![openai](doc/openai.jpg)
   
   * 邀请用户为嘉宾,获取知识星球的cookie(ZSXQ_COOKIE)
   
   ![星球cookie](doc/%E6%98%9F%E7%90%83cookie.jpg)
   
   * 获取知识星球的id(ZSXQ_GROUP_ID)
   
   ![星球groupid](doc/%E6%98%9F%E7%90%83groupid.jpg)

将上面拿到的信息填入下面配置文件

```yaml
spring:
  profiles:
    active: ${SPRING_PROFILES_ACTIVE:prod}
  task:
    scheduling:
      pool:
        size: 5
server:
  port: 8080
openai:
  model: ${OPENAI_MODEL:gpt-3.5-turbo}
  apiKey: ${OPENAI_API_KEY:你的apiKey}
zsxq:
  cookie: ${ZSXQ_COOKIE:你的星球cookie}
  groupId: ${ZSXQ_GROUP_ID:你的星球id}
  silenced: ${ZSXQ_SILENCED :true}
scheduler:
  list:
    - name: chatbotTask
      platform: zsxq
      answer: openai
      cron: '0/30 * * * * ?'
#    - name: demoTask
#      platform: demo
#      answer: demo
#      cron: '0/10 * * * * ?'
```

2. 运行`start`模块下的`Application`就可以开始定时任务的调度啦🎉

## 一键部署

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/6-WHtb)


