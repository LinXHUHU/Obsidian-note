
项目背景：zcu 右驱 开发板DV测试

项目需求:
EE耐久测试需求
{
一次完整的测试有11 个 cycle，每个cycle 持续的时间分别为，
cycle1 5s，靠近解锁工况
cycle2 5s, 驻车1
cycle3 10s, 驻车2
cycle4 5s, 转弯或起伏路面
cycle515s, 白天+夏季行驶
cycle6 15s,  白天+雾天行驶
cycle7 15s, 夜间+冬季行驶
cycle8 15s, 夜间+雨天行驶
cycle9 5s,  离车
cycle10 5s, 休眠
cycle11 5s 唤醒
}

EMC测试需求
{
	又分为EMS 和 EMI工况
	EMS需求
	{
		EMS-1 400ms，
		EMS-2 400ms,
		EMS-3 400ms,
		EMS-4 400ms,
		EMS-5 400ms
	}
	EMI需求
	{
		就一个EMI
	}
}
