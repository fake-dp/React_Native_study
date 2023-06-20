## IOS & Android 스타일링 차이

우선 주의 할점은 네이티브는 웹처럼 연속적으로 스타일이 적용되지 않는다. 그래서 해당 컴포넌트에 따로 스타일을 적용하는 것이 바람직하다.

그리고 모든 플렛폼에서 문제없이 작동하려면 코드를 조정해야 하는 경우가 있다. ios에서는 둥근 모서리를 Text컴포넌트에 직적 하면 적용되지 않는 문제가 있다. 그이유는 ios의 텍스트 요소의 볼더가 지원되지 않기 때문이다. 될수 있으면 View와 Text를 분리해서 스타일을 적용하는것이 좋다.

<br />

### 예시 코드

```js
// 모든 플렛폼에서 지원 안됨
 <View style={styles.goalsContainer}>
        <Text>Goal List...</Text>
        {courseGoals.map((goal, index) => (
            <Text style={styles.goalItem} key={index}>{goal}</Text>
        ))}
</View>

// 모든 플렛폼에서 지원 됨
// view와 text를 분리해서 적용했기 때문
<View style={styles.goalsContainer}>
        <Text>Goal List...</Text>
        {courseGoals.map((goal, index) => (
          <View style={styles.goalItem} key={index}>
            <Text style={styles.goalText}>{goal}</Text>
          </View>
        ))}
</View>
```
