# state-grid-multiple
多电表版国家电网用电信息青龙脚本，配合mqtt，在homeassistant中统计  

----

当前为多电表版，单电表版请点击👉[查看详情](./README.md)

----


## 青龙设置  
使用state-grid-multiple.js，其他同单电表版
### 青龙环境变量设置  
同单电表版 
## homeassistant设置参考  
订阅主题: nodejs/state-grid/1111111111111、nodejs/state-grid/2222222222222  
1111111111111、2222222222222自行替换为实际用电户号  
configuration.yaml 文件添加mqtt传感器
```
mqtt:
  sensor:
    - name: "电费余额"
      icon: 'mdi:lightning-bolt'
      unique_id: 'yong_dian_xin_xi_1111111111111'
      state_topic: "nodejs/state-grid/1111111111111"
      value_template: "{{ value_json.sumMoney }}"
      unit_of_measurement: '元'
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 1'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[0].dayElePq }}'
      unique_id: "electricity_usage_day1_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[0] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 2'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[1].dayElePq }}'
      unique_id: "electricity_usage_day2_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[1] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 3'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[2].dayElePq }}'
      unique_id: "electricity_usage_day3_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[2] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 4'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[3].dayElePq }}'
      unique_id: "electricity_usage_day4_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[3] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 5'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[4].dayElePq }}'
      unique_id: "electricity_usage_day5_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[4] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 6'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[5].dayElePq }}'
      unique_id: "electricity_usage_day6_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[5] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: 'Electricity Usage Day 7'
      state_topic: 'nodejs/state-grid/1111111111111'
      value_template: '{{ value_json.dayList[6].dayElePq }}'
      unique_id: "electricity_usage_day7_1111111111111"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/1111111111111"
      json_attributes_template: "{{ value_json.dayList[6] | tojson }}"
      device:
        identifiers: ["mqtt1111111111111"]
        name: "用电信息-1111111111111"
    - name: "电费余额"
      icon: 'mdi:lightning-bolt'
      unique_id: 'yong_dian_xin_xi_2222222222222'
      state_topic: "nodejs/state-grid/2222222222222"
      value_template: "{{ value_json.sumMoney }}"
      unit_of_measurement: '元'
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 1'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[0].dayElePq }}'
      unique_id: "electricity_usage_day1_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[0] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 2'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[1].dayElePq }}'
      unique_id: "electricity_usage_day2_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[1] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 3'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[2].dayElePq }}'
      unique_id: "electricity_usage_day3_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[2] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 4'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[3].dayElePq }}'
      unique_id: "electricity_usage_day4_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[3] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 5'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[4].dayElePq }}'
      unique_id: "electricity_usage_day5_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[4] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 6'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[5].dayElePq }}'
      unique_id: "electricity_usage_day6_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[5] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
    - name: 'Electricity Usage Day 7'
      state_topic: 'nodejs/state-grid/2222222222222'
      value_template: '{{ value_json.dayList[6].dayElePq }}'
      unique_id: "electricity_usage_day7_2222222222222"
      device_class: "energy"
      unit_of_measurement: "度"
      icon: "mdi:chart-bell-curve"
      json_attributes_topic: "nodejs/state-grid/2222222222222"
      json_attributes_template: "{{ value_json.dayList[6] | tojson }}"
      device:
        identifiers: ["mqtt2222222222222"]
        name: "用电信息-2222222222222"
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
        entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
        name: 电费余额
        attribute: sumMoney
        unit: 元
        icon: mdi:currency-usd
      - type: entity
        entity: sensor.yong_dian_xin_xi_1111111111111_electricity_usage_day_1
        name: 昨日用电
        icon: mdi:lightning-bolt
      - type: entity
        entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
        name: 年度总电费
        attribute: totalEleCost
        unit: 元
        icon: mdi:currency-usd
      - type: entity
        entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
        name: 年度总电量
        unit: 度
        icon: mdi:lightning-bolt
    square: false
  - type: entity
    entity: sensor.yong_dian_xin_xi_1111111111111_electricity_usage_day_1
    name: 昨日日期
    attribute: day
    icon: mdi:calendar-today
  - type: entity
    entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
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
  include: sensor.yong_dian_xin_xi_1111111111111_electricity_usage_day*
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
  - entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
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
  - entity: sensor.yong_dian_xin_xi_1111111111111_dian_fei_yu_e
    name: 用电量
    unit: 度
    type: column
    data_generator: |
      return entity.attributes.monthList.map((peak, index) => {
        return [entity.attributes.monthList[index].endDate, entity.attributes.monthList[index].monthEleNum];
      });

```
