# JmEGamePad 1.2 #
### GamePad Library for Android Games running java/Kotlin ###

[![](https://jitpack.io/v/Scrappers-glitch/JmEGamePad.svg)](https://jitpack.io/#Scrappers-glitch/JmEGamePad)

## [Video about this Library ](https://youtu.be/-fifyREL2Yo) ##
## [JmeGamePad on a JmeVehiclesExample,Example of Responsive layout](https://youtu.be/LZkmWAvh9j0) ##

##### How to implement it into your Android project :

Step 1. Add it in your root build.gradle at the end of repositories :
```gradle
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
  ```

Step 2. Add the dependency :
```gradle
	dependencies {
	        implementation 'com.github.Scrappers-glitch:JmEGamePad:1.2'
	}
```
Step 3. If you are using JME(JmonkeyEngine3.3.2-Stable) then :

## 1-> Create a class extending GameStickView : ##
```java

import android.annotation.SuppressLint;
import android.app.Activity;

import com.jme3.app.SimpleApplication;
import com.scrappers.jmeGamePad.GameStickView;


@SuppressLint("ViewConstructor")
public class GameStick extends GameStickView {
    
    private VehicleControl vehicleControl;
    private final SimpleApplication jmeContext;

    public GameStick(Activity appCompatActivity, SimpleApplication jmeContext) {
        super( appCompatActivity);
        this.jmeContext=jmeContext;

    }


    @Override
    public void accelerate(final float pulse) {
        jmeContext.enqueue(new Runnable() {
            @Override
            public void run() {
		//some jme code
            }
        });

    }

    @Override
    public void reverseTwitch(float pulse) {
        jmeContext.enqueue(new Runnable() {
            @Override
            public void run() {
		//some jme code
            }
        });

    }

    @Override
    public void steerRT(final float pulse) {
        jmeContext.enqueue(new Runnable() {
            @Override
            public void run() {
		//some jme code
            }
        });

    }

    @Override
    public void steerLT(final float pulse) {
        jmeContext.enqueue(new Runnable() {
            @Override
            public void run() {
		//some jme code
            }
        });

    }

    @Override
    public void neutralizeState(float pulseX, float pulseY) {
        jmeContext.enqueue(new Runnable() {
            @Override
            public void run() {
		//some jme code            
            }
        });

    }


}
```

## 2-> Do something like that in your game context class or another gameState : ##

```java

import android.graphics.Color;
import android.view.View;

import com.jme3.app.SimpleApplication;
import com.jme3.asset.AssetManager;
import com.jme3.scene.Node;
import com.scrappers.jmeGamePad.GamePadView;

public class JmeGame extends SimpleApplication {
    @Override
    public void simpleInitApp() {
        /*LIBRARY CODE*/
        /*run the gamePad Attachments & listeners from the android activity UI thread */
        JmeHarness.jmeHarness.runOnUiThread(new Runnable() {
            @Override
            public void run() {
                /* create an instance of a class extending gameStickView to easily handle the listeners */
                GameStick gameStick = new GameStick(JmeHarness.jmeHarness,JmeGame.this);
                /* set the vehicle Control */
                gameStick.setVehicleControl(vehicle);
                /* create a gamePadView instance of cardView/FrameLayout to display gamePad Component */
                GamePadView gamePadView=new GamePadView( JmeHarness.jmeHarness,gameStick);
                /* Initialize GamePad Parts*/
                gamePadView.initializeGamePad(R.drawable.gamepad_domain,GamePadView.ONE_THIRD_SCREEN)
                         .initializeGameStickHolder(R.drawable.moving_stick_domain)
                         .initializeGameStick(GamePadView.CRYSTAL_BUTTONS,R.drawable.ic_baseline_gamepad_24,200);
                /*initialize the gameStick track */
                gamePadView.setMotionPathColor(Color.BLACK);
                gamePadView.setMotionPathStrokeWidth(10);
                gamePadView.setStickPathEnabled(true);
                /* initialize pad buttons & listeners A,B,X,Y */
                gamePadView.addControlButton("BUTTON A",GamePadView.GAMEPAD_BUTTON_A ,GamePadView.CRYSTAL_BUTTONS, R.drawable.ic_baseline_gamepad_24,new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

}
                },null);
                gamePadView.addControlButton("BUTTON B",GamePadView.GAMEPAD_BUTTON_B , GamePadView.CRYSTAL_BUTTONS, R.drawable.ic_baseline_gamepad_24,new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

                    }
                },null);
                gamePadView.addControlButton("BUTTON X",GamePadView.GAMEPAD_BUTTON_X , GamePadView.CRYSTAL_BUTTONS, R.drawable.ic_baseline_gamepad_24,new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

}
                },null);
                gamePadView.addControlButton("BUTTON Y",GamePadView.GAMEPAD_BUTTON_Y , GamePadView.CRYSTAL_BUTTONS, R.drawable.ic_baseline_gamepad_24,new View.OnClickListener() {
                    @Override
                    public void onClick(View view) {

}
                },null);

            }
        });
    }



    @Override
    public void simpleUpdate(float tpf) {
    }

}

```




Images :

CRYSTAL BUTTONS ONE_THIRD_SCREEN Config

![ONE_THIRD_SCREEN Config](https://i.imgur.com/qIvQhOw.png)

CRYSTAL BUTTONS HALF_SCREEN Config

![HALF_THIRD_SCREEN Config](https://i.imgur.com/z4FkJi9.png)

MATERIALISTIC BUTTONS ONE_THIRD_SCREEN Config

![MATERIALISTIC BUTTONS ONE_THIRD_SCREEN Config](https://i.imgur.com/EA5XKSE.png)

DEFAULT BUTTONS QUARTER_SCREEN Config

![QUARTER_SCREEN Config](https://i.imgur.com/gEo45K2.png)



