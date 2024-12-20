# state-grid
国家电网青龙脚本，配合mqtt，在homeassistant中统计  

<img width="1057" alt="image" src="https://github.com/user-attachments/assets/b8e3986a-718f-4adb-ab2c-e199c7e6f114" />

## 青龙设置  
青龙需安装mqtt依赖  
### 青龙环境变量设置  

```
 export WSGW_USERNAME="" #网上国网账号
 export WSGW_PASSWORD="" #网上国网密码
 export WSGW_RECENT_ELC_FEE="true" #是否获取最近电费
 export WSGW_mqtt_host="" #mqtt服务器地址 192.168.1.7
 export WSGW_mqtt_port="" #mqtt服务器端口 1883
 export WSGW_mqtt_username="" #mqtt服务器用户名
 export WSGW_mqtt_password="" #mqtt服务器密码
```
## homeassistant设置参考  
订阅主题: nodejs/state-grid  
configuration.yaml 文件添加mqtt传感器
```
mqtt:
  sensor:
    - name: "电费余额"
      icon: 'mdi:lightning-bolt'
      unique_id: 'yong_dian_xin_xi'
      state_topic: "nodejs/state-grid"
      value_template: "{{ value_json.sumMoney }}"
      unit_of_measurement: '元'
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json | tojson }}"
    - name: 'Electricity Usage Day 1'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[0].dayElePq }}'
      unique_id: "electricity_usage_day1"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[0] | tojson }}"
    - name: 'Electricity Usage Day 2'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[1].dayElePq }}'
      unique_id: "electricity_usage_day2"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[1] | tojson }}"
    - name: 'Electricity Usage Day 3'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[2].dayElePq }}'
      unique_id: "electricity_usage_day3"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[2] | tojson }}"
    - name: 'Electricity Usage Day 4'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[3].dayElePq }}'
      unique_id: "electricity_usage_day4"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[3] | tojson }}"
    - name: 'Electricity Usage Day 5'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[4].dayElePq }}'
      unique_id: "electricity_usage_day5"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[4] | tojson }}"
    - name: 'Electricity Usage Day 6'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[5].dayElePq }}'
      unique_id: "electricity_usage_day6"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[5] | tojson }}"
    - name: 'Electricity Usage Day 7'
      state_topic: 'nodejs/state-grid'
      value_template: '{{ value_json.dayList[6].dayElePq }}'
      unique_id: "electricity_usage_day7"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid"
      json_attributes_template: "{{ value_json.dayList[6] | tojson }}"
  ```
## homeassistant卡片参考  
用电概况统计
```
type: vertical-stack
cards:
  - type: grid
    columns: 2
    cards:
      - type: entity
        entity: sensor.dian_fei_yu_e
        name: 电费余额
        attribute: sumMoney
        unit: 元
        icon: mdi:currency-usd
      - type: entity
        entity: sensor.electricity_usage_day_1
        name: 昨日用电
        icon: mdi:lightning-bolt
      - type: entity
        entity: sensor.dian_fei_yu_e
        name: 年度总电费
        attribute: totalEleCost
        unit: 元
        icon: mdi:currency-usd
      - type: entity
        entity: sensor.dian_fei_yu_e
        name: 年度总电量
        attribute: totalEleNum
        unit: 度
        icon: mdi:lightning-bolt
    square: false
  - type: entity
    entity: sensor.electricity_usage_day_1
    name: 昨日日期
    attribute: day
    icon: mdi:calendar-today
  - type: entity
    entity: sensor.dian_fei_yu_e
    name: 更新日期
    attribute: amtTime
    icon: mdi:clock-time-three
title: 用电统计

```
过去7天用电情况，没有峰谷电价，电价按0.4883计算
```
type: custom:flex-table-card
title: 过去7天用电情况
entities:
  include: sensor.electricity_usage_day*
columns:
  - name: 日期
    data: day
  - name: 用电量
    data: state
    suffix: 度
  - name: 电费
    data: state
    modify: parseFloat(x*0.4883).toFixed(2)
    suffix: 元

```
最近日用电图表  
```
type: custom:apexcharts-card
graph_span: 10d
span:
  end: day
header:
  show: true
  title: 最近10天电量统计数据
  show_states: true
  colorize_states: true
series:
  - entity: sensor.dian_fei_yu_e
    name: 用电量
    unit: 度
    type: column
    float_precision: 2
    data_generator: |
      return entity.attributes.dayList.reverse().map((peak, index) => {
        return [entity.attributes.dayList[index].day, entity.attributes.dayList[index].dayElePq];
      });
yaxis:
  - min: 0

```
月用电图表  
```
type: custom:apexcharts-card
graph_span: 12month
header:
  show: true
  title: 最近12个月电量统计数据
  show_states: true
  colorize_states: true
series:
  - entity: sensor.dian_fei_yu_e
    name: 用电量
    unit: 度
    type: column
    data_generator: |
      return entity.attributes.monthList.map((peak, index) => {
        return [entity.attributes.monthList[index].endDate, entity.attributes.monthList[index].monthEleNum];
      });

```
