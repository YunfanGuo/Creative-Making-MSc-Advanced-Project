# Creative-Making-MSc-Advanced-Project-Blog

github link:https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/tree/main
## Introduction
In modern society, although the rapid development of technology has provided us with more convenience, however, people's perception of time in daily life is facing new challenges. Social media, digital entertainment, and fast-paced work life make people tend to get lost in the passage of time. This fuzzy sense of time may lead to individual troubles in time management, affecting life efficiency and satisfaction. Therefore, I hope to design and produce an interactive device to trigger people's perception of the passage of time.

Although I thought there might be many fatal problems with the project and that the final product might feel differently than it was designed to, luckily, it achieved the effect I wanted. Moreover, I learned a lot from the project. This includes using the various tools at school, learning techniques, etc. I want to thank all the students and teachers who have inspired and helped me during the project.

## Stage 1 Finding relevant information and designing the device
After reviewing a range of literature on the passage of time, I wanted to make a device similar to an hourglass. But different from an hourglass because it is not unilateral like an hourglass where only the visual part exists and a single action of going down the hourglass is performed directly. The device aims to guide participants to be more aware of the passage of time through multi-sensory stimuli of sight, sound and touch. I plan to use an Arduino to program the functional logic that will control the operation of the device. Below is a diagram of my design.

![IMG_9028](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/908636f1-c9cc-445b-9ce8-f2540fa1be02)

![IMG_8966(20231120-173514)](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/365e479d-3634-4180-a82d-9baeed0a3c86)

The device has two main parts.

1. The ultrasonic sensor controls the rotation of the fan and the display of information on the OLED screen. When it detects that someone is in range, the fan starts to rotate, driving the fine sand flying. The OLED screen displays the participant's participation time and tells the participant how many seconds of his life he has spent watching this device.

2. Control the LED strip light on and off and audio music playback through the switch.

## Stage 2 Selection of suitable materials and equipment
The basic frame of the device uses clear acrylic sheet because of his high light transmission strength. It was the perfect fit for the device and I used the school's laser cutter to cut the sheet.

![IMG_9029](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/74ffd383-0f5b-40c6-8fe1-2b6929c63dbd)

Fans After many tests choose a fan for small domestic extraction. It has a high air speed and is adjustable for the amount of airflow. It serves well for subsequent tests on which air speed is better to use.

![IMG_9035](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/c50330d0-67c7-4851-a855-d29f4ef6e2b6)

The screen uses a colourful high display OLED screen. The light strip uses ordinary LED light strips with adjustable light brightness.

![IMG_9034(20231108-154022)](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/ead1e727-5ac9-4f92-b419-dbd3e91143c6)

![IMG_9036](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/02c5fe23-d9c6-475a-9e9b-c63f3aeb2821)

## Stage 3 code design and circuit soldering
Because I am very comfortable with writing code, I start writing code directly from the logic of the implementation. This is something I am better at. I will write the adjustable parameters and pins in the front and clearly label the comments to make it easier for me to adjust the device values later.

`pinMode(4, OUTPUT);   //Ultrasonic trig feet `

`pinMode(5, INPUT);    //Ultrasonic ECHO feet`

`pinMode(6, OUTPUT);   //Fan Relay`

`pinMode(7,INPUT_PULLUP);//Light Strip Brightness +`

`pinMode(8,INPUT_PULLUP);//Light Strip Brightness -`

`pinMode(9,INPUT_PULLUP);//Speaker Switch`

`pinMode(2,OUTPUT);//speakers`

`pinMode(10,OUTPUT);//light strip PWM`

The following code shows the logic for controlling the pattern display and text display of an OLED screen, and the logic for switching the fan on and off via an ultrasonic sensor.

```
timer.run();    //Enable Timer Count

  if (millis() - t > 300) {   //Refresh every 300 milliseconds

    item = checkdistance_4_5();   //Read ultrasound

    if (item <= 150) {   //Less than 150 cm is considered close
      digitalWrite(6, HIGH);
      u8g2.firstPage();
      do
      {
        u8g2.setFont(u8g2_font_timR10_tf);
        u8g2.setFontPosTop();
        u8g2.setCursor(0, 0);
        u8g2.print("You've spent");
        u8g2.setCursor(0, 15);
        u8g2.print(String(i) + String("  seconds"));
        u8g2.setCursor(0, 30);
        u8g2.print("of your life watching");
        u8g2.setCursor(0, 45);
        u8g2.print("this installation.");
      } while (u8g2.nextPage());

    } else {    //People leaving the front of the unit
      i = 0;
      digitalWrite(6, LOW);   //fan shutdown
      u8g2.firstPage();
      do
      {
        u8g2.drawXBMP(52, 12, 24, 40, bitmap);    //Show Hourglass Pattern
      } while (u8g2.nextPage());
    }

    t = millis();
  }
```

Below is a diagram of the logical wiring and the soldering process.

![IMG_9014](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/695aa7bf-4626-4ef3-a3bb-dc6164d90226)

![IMG_9033](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/5e35c9cf-c96c-4539-b8b1-58ded267a09b)

![IMG_9031(20231110-134325)](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/13b57c6b-8ff8-4525-82fd-8e98b383ff42)

![IMG_9037](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/4c5b35a1-649a-4313-a971-2d2b89bb1dd6)

## Stage 4 assembly and experimentation of the device
Whilst I had implemented all the features and planned how to build the exterior, I still encountered a number of difficulties in the actual construction. For example, the wind power of the fan needed a series of adjustments, and the wind speed was not suitable to be too high; too high would cause the sand grains inside the device to fly too fast, thus preventing the viewer from seeing the details of the process. Too slow wind speed will lead to sand particles not flying in the first layer of the device. The sand particles need to be of a size and weight that is not too large or too small, as they will also affect the viewing experience of the viewer. Through continuous testing, I found the most suitable sand size and wind speed. The ultrasonic sensor was finally selected to have a sensing distance of 1.5m because within this distance the participants could hear the sound of the sand particles hitting the side wall of the device, and the viewing effect was clearer and more immersive, which made the experience the best. The background music was chosen to be Hans Zimmer's "Cornfield Chase" and "Time" after much deliberation. Because "Cornfield Chase" was used in the film "Star Trek", this song can bring people a feeling of time travelling in the universe. The other track "Time" was used in the film "Inception" as the ending song, which will bring a strong sense of time immersion.

![IMG_9030(20231102-160956)](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/432a625b-0050-4057-b558-f891f7ac27bd)

![CEEA3E92EA4273E52B1A0F5DDB0D7769](https://github.com/YunfanGuo/Creative-Making-MSc-Advanced-Project/assets/119873151/64b133f1-7494-4da1-86a5-0ad847978a47)

For the experimental part, I have indoors inviting people to come and watch the experience.I do not provide any hints about the theme of the installation until the visitors have experienced it. After their visit, I will interview them and ask them how they feel about it. I make a textual record of their feelings. Regardless of whether their feelings are relevant to my theme or not, I will tell them the theme I want to express in the installation after they share their feelings. If there are feelings that do not fit the theme, I will explain the theme of the installation after the participants have finished speaking, and then I will ask the visitors again if their feelings have changed, and if they have, I will record the new feelings again. After obtaining the feelings of different participants, I will analyze each person's feelings and draw conclusions about each participant's feelings. I will also summarise the ideas that emerge from the feelings. I also asked each participant to count the length of their experience without looking at the screen before starting the tour and finally compare it to the actual length of the experience on the screen (The test experience lasts for two minutes and an enquiry will be recorded when the time is up.). In the Documentation section there is added text recorded in the Interviews section.

Below is a link to a demo video I recorded about this device.

https://youtu.be/uY33vVXsSnc
