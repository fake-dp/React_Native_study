## ScrollView

리엑트와 달리 네이티브는 스크롤 기능 구현이 매우 쉽다. 네이티브에서 제공해주기 때문이다. 다만 적용 할때는 무조건 해당 영역 안에 태그를 넣어서 적용해야한다. 그렇지 않으면 플랙스 영역이 다깨지기 때문이다. 이점만 주의 하면 된다.

<br />

### 예시코드

```js
<View style={styles.goalsContainer}>
  <ScrollView alwaysBounceVertical={true}>
    {courseGoals.map((goal, index) => (
      <View style={styles.goalItem} key={index}>
        <Text style={styles.goalText}>{goal}</Text>
      </View>
    ))}
  </ScrollView>
</View>
```

<br />

## FlatList 최적화

아마 스크를 뷰 보다 많이 쓰일 컴포넌트다. 이컴포넌트를 사용하면 최적화가 가능하다. 만약 10~20개의 데이터가 별로 없으면 스크롤뷰를 사용하면 되겠지만, 용량이 많고 데이터가 유동적이면 FlatList를 사용하는 것을 권장한다.

<br />

### 예시코드

```js
// scrollview 대신 작성한 것이다.
// data는 말그대로 전체 데이터
// renderItem은 뿌려줄 데이터 리스트
// KeyExtractor는 해당 고유 아이디값 설정
<FlatList
  data={courseGoals}
  alwaysBounceVertical={false}
  renderItem={(itemData) => (
    <View style={styles.goalItem}>
      <Text style={styles.goalText}>{itemData.item.text}</Text>
    </View>
  )}
  keyExtractor={(item) => item.id}
/>
```

여기서 데이터는 객체 형태로 받아 오는 것이 좋다. item은 네이티브에서 제공한 내장 객체이다. 콘솔 찍으면 확인할 수 있다.
동적 데이터를 가진 목록을 스크롤이 가능하도록 만들려면 FlatList를 사용하자 성능면에서 아주 좋으니까 !
