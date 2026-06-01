# MQTT 客户端
- - -

`ruoyi-common-mqtt` 基于 mica-mqtt 封装 MQTT 客户端接入，并使用 JDK 21 虚拟线程优化客户端线程模型。

## 模块位置

```text
ruoyi-common/ruoyi-common-mqtt
```

主要类：

```text
org.dromara.common.mqtt.config.MqttAutoConfiguration
org.dromara.common.mqtt.listener.MqttClientConnectListener
org.dromara.common.mqtt.listener.MqttClientGlobalMessageListener
```

## 配置方式

在需要接入 MQTT 的服务配置中增加：

```yaml
mqtt.client:
  enabled: true
  ip: 127.0.0.1
  port: 1883
  name: Mqtt-Client
  client-id: 000001
  username: ruoyi
  password: 123456
```

## 监听逻辑

全局消息监听器：

```text
MqttClientGlobalMessageListener
```

默认会记录所有订阅消息。实际业务中可以替换或扩展监听器，将 MQTT 消息转为业务事件、设备状态、告警消息或统一推送。

## 使用建议

- `client-id` 必须唯一，生产环境不要多个实例共用同一个客户端 ID。
- MQTT Server 可以使用 EMQX、Mosquitto 或 mica-mqtt server。
- 设备消息进入系统后，如需推送给前端，建议通过 [统一消息推送](/6.X/ruoyi-cloud-plus/framework/extend/message_push.md) 发送。
