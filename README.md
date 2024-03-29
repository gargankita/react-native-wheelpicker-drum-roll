# react-native-wheelpicker-drum-roll

## Introduction
Cross platform Picker component based on React-native.

Since picker is originally supported by ios while Android only supports a ugly Spinner component. If you want to have the same user behaviour, you can use this.


## How to use

Run command

For apps using RN 0.40 or higher, please run
```
npm i react-native-wheelpicker-drum-roll --save
```
For apps using RN 0.39 or less, please run
```
npm install --save --save-exact react-native-wheelpicker-drum-roll@1.0.0
```
Add in settings.gradle
```
include ':react-native-wheelpicker-drum-roll'
project(':react-native-wheelpicker-drum-roll').projectDir = new File(settingsDir, '../node_modules/react-native-wheelpicker-drum-roll/android')
```
Add in app/build.gradle
```
implementation project(':react-native-wheelpicker-drum-roll')
```
Modify MainApplication
```
    import com.zyu.ReactNativeWheelPickerPackage;
    ......

    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            new MainReactPackage(), new ReactNativeWheelPickerPackage()
        );
    }
```

## Example code
```
import React, { Component } from 'react';
import {
	Platform,
	StyleSheet,
	Text,
	View,
} from 'react-native';


import Picker from 'react-native-wheelpicker-drum-roll'
var PickerItem = Picker.Item;

export default class App extends Component<{}> {

	constructor(props) {
		super(props);
		this.state = {
			selectedItem : 2,
			itemList: ['刘备', '张飞', '关羽', '赵云', '黄忠', '马超', '魏延', '诸葛亮']
		};
	}

	onPickerSelect (index) {
		this.setState({
			selectedItem: index,
		})
	}

	onAddItem = () => {
		var name = '司马懿'
		if (this.state.itemList.indexOf(name) == -1) {
			this.state.itemList.push(name)
		}
		this.setState({
			selectedItem: this.state.itemList.indexOf(name),
		})
	}

	render () {
		return (
			<View style={styles.container}>
				<Text style={styles.welcome}>
					Welcome to React Native!
				</Text>
				<Picker style={{width: 150, height: 180}}
					selectedValue={this.state.selectedItem}
					itemStyle={{color:"white", fontSize:26}}
					onValueChange={(index) => this.onPickerSelect(index)}>
						{this.state.itemList.map((value, i) => (
							<PickerItem label={value} value={i} key={"money"+value}/>
						))}
				</Picker>
				<Text style={{margin: 20, color: '#ffffff'}}>
					你最喜欢的是：{this.state.itemList[this.state.selectedItem]}
				</Text>

				<Text style={{margin: 20, color: '#ffffff'}}
						onPress={this.onAddItem}>
			怎么没有司马懿？
				</Text>
			</View>
		);
	}
}

const styles = StyleSheet.create({
	container: {
		flex: 1,
		justifyContent: 'center',
		alignItems: 'center',
		backgroundColor: '#1962dd',
	},
	welcome: {
		fontSize: 20,
		textAlign: 'center',
		margin: 10,
		color: '#ffffff',
	},
	instructions: {
		textAlign: 'center',
		color: '#333333',
		marginBottom: 5,
	},
});
```
