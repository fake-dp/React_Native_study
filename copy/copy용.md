## 복사용 파일

```js
//app
import { StyleSheet, ImageBackground,SafeAreaView } from 'react-native';
import StartGameScreen from './screens/StartGameScreen';
import {LinearGradient} from 'expo-linear-gradient';
import { useState } from 'react';
import GameScreen from './screens/GameScreen';
export default function App() {

  const [userNumber, setUserNumber] = useState();


  function pickedNumberHandler(pickedNumber){
    setUserNumber(pickedNumber);
  }


  let screen = <StartGameScreen onPickNumber={pickedNumberHandler}/>

  if(userNumber){
    screen = <GameScreen userChoice={userNumber}/>
  }

  return (
    <LinearGradient
    colors={["#4e0329","#ddb52f"]}
      style={styles.rootScreen}
    >
      <ImageBackground source={require('./assets/images/background.png')
    }
    resizeMode='cover'
    imageStyle={styles.backgroundImage}
    style={styles.rootScreen}
    >
      <SafeAreaView
      style={styles.myrootScreen}
      >{screen}</SafeAreaView>
  {/* {screen} */}
      </ImageBackground>
    </LinearGradient>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex:1,
    backgroundColor: "#ddb52f",
  },
  backgroundImage:{
    opacity: 0.5,
  },
  myrootScreen:{
    flex:1,
  },

});

```

```js
// startgame
import { useState } from "react";
import { TextInput, View, StyleSheet ,Alert} from "react-native";
import PrimaryButton from "../components/PrimaryButton";
function StartGameScreen({onPickNumber}) {

    const [enterdNumber, setEnteredNumber] = useState("")

    function numberInputHandler(enterText){
        console.log(enterText)
        setEnteredNumber(enterText);
    }

    function resetInputHandler(){
        setEnteredNumber("");
    }

    function confirmInputHandler(){
        const chosenNumber = parseInt(enterdNumber);

        if(isNaN(chosenNumber) || chosenNumber <= 0 || chosenNumber > 99){
            Alert.alert("Invalid number!", "Number has to be a number between 1 and 99.", 
            [{text: "Okay", style: "destructive", onPress: resetInputHandler}])
            return;
        }
        onPickNumber(chosenNumber);
    }


    return <View style={styles.inputContainer}>
            <TextInput 
            value={enterdNumber}
            onChangeText={numberInputHandler}
            style={styles.numberInput}
            maxLength={2}
            keyboardType="number-pad"

            //자동 대문자 변환
            autoCapitalize="none"
            //자동 수정 기능
            autoCorrect={false}
            />
            <View style={styles.buttonsContainer}>
            <View style={styles.buttonContainer}>
            <PrimaryButton onPress={resetInputHandler}>reset</PrimaryButton>
            </View>
            <View style={styles.buttonContainer}>
            <PrimaryButton onPress={confirmInputHandler}>confirm</PrimaryButton>
            </View>
            </View>
        </View>
    
}

export default StartGameScreen;


const styles = StyleSheet.create({
    inputContainer: {
        // flex: 1,
        justifyContent: "center",
        alignItems: "center",
        padding: 16,
        marginTop: 100,
        marginHorizontal: 24,
        backgroundColor: "#4e0329",
        borderRadius: 8,
        //안드로이드 그림자효과
        elevation: 4,

        //ios 그림자효과
        shadowColor: "black",
        shadowOffset: {
            width: 0,
            height: 2,
        },
        shadowRadius: 6,
        shadowOpacity: 0.25,
    },
    numberInput: {
        height: 50,
        borderBottomColor: "#ddb52f",
        borderBottomWidth: 1,
        color: "#ddb52f",
        fontSize: 32,
        marginVertical: 8,
        fontWeight: "bold",
        width: 50,
        textAlign: "center",
    },
    buttonsContainer: {
        flexDirection: "row",
    },
    buttonContainer:{
        flex:1,
    },
})
```

```js
// com/primary
import { View, Text, Pressable, StyleSheet } from "react-native";

function PrimaryButton({children, onPress}){


// android ripple는 클릭시 물결효과 

    return(
        <View style={styles.buttonOuterContainer}>
        <Pressable 
        style={({pressed})=> pressed ? [
            styles.buttonInnerContainer, styles.pressed
        ]: styles.buttonInnerContainer}
        onPress={onPress} android_ripple={{
            color:'#640233'
    }}>
            <Text
            style={styles.buttonText}
            >{children}</Text>
        </Pressable>
        </View>
    )
}

export default PrimaryButton;

const styles = StyleSheet.create({
    buttonOuterContainer:{
        borderRadius: 28,
        margin: 4,
        overflow: "hidden",
    },
    buttonInnerContainer:{
        backgroundColor: "#72063c",
        borderRadius: 28,
        paddingVertical: 8,
        paddingHorizontal: 16,
        elevation: 4,
        margin:4,
    },
    buttonText:{
        color: "#fff",
        textAlign: "center",
    },
    //물결효과는 안드로이만 있음 그래서 ios는 따로 설정
    pressed:{
        opacity: 0.75,
    }
})
```

```js
// gamescreen
import { View, Text, StyleSheet, } from 'react-native';

function GameScreen(){
    return(
        <View style={styles.screen}>
            <Text style={styles.title}>Opponents's Guess</Text>
       <View>

            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
            <Text>Opponents's Guess</Text>
       </View>
        </View> 
    );
}

export default GameScreen;

const styles = StyleSheet.create({
  screen: {
    flex: 1,
    padding: 24,
  },
  title:{
        fontSize: 18,
        fontWeight: "bold",
        color: "#ddb52f",
        textAlign: 'center',
        borderWidth: 2,
        borderColor: "#ddb52f",
        borderRadius: 1,
  }
})

```