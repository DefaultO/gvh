![grafik](https://github.com/user-attachments/assets/396806ef-1e8f-4337-bcbe-a9c3a038785e)

# Goodbye Volcano High (GVH) Modding Project

## Game Info
Game: [**Goodbye Volcano High**](https://store.steampowered.com/app/1310330/Goodbye_Volcano_High/)<br/>
Playtime: 5-6 hours<br/>
Engine: **Unity 2021.3.18f1** (*mono*)<br/>
Binary of Interest: ``...\Goodbye Volcano High\Goodbye Volcano High_Data\Managed\Gvh.dll``<br/>
Protections: None.

## Features I want to focus on:
- making the rythm minigame playable using custom beatmaps, perhaps automap-functionality for osu beatmaps and other popular rythm game beatmap formats
- fixing (missing words in) subtitles
- fixing abrupt audio cuts (if they don't come pre-cut like that)
- adding a restart button in the pause menu for the minigame (story)
- way in the future, multiple saves and or time-warp functionality (go back to events that already occured, preferably using a slider with images similiar to a video player, but that's a problem for future me)
- way in the future an easy modding framework like everest for celeste. so that people can develop their own fan-fiction or add their own features to the base game.

## Why do I do this?
the people that paid the full price for this game deserve more. I got it for just under 20€ and think that additions like these would be so easy to develop/design if you had access to the unity project. it would bring so much extra-content/replayability to the game that it kinda annoys me that I have to figure everything out by myself while developing a full-fledged melonloader mod for this. you can't imagine how hard it is to reuse the ui components of the game and design some user interface/scene with it using code alone.

## Release when?
idk. won't work on the mod all the time. won't have motivation to continue every day. it's a slow process that will take its time. so no eta. it is ready when it is ready. first release comes when the mod has user-generated beatmap support.

## Update 1.0.0
figured out how to customize the title screen. so I added a few buttons.

idk why, but...<br/><br/>
a) I wasn't able to get most of the ui gameobjects directly. they didn't appear when using the GameObject.Find... methods. so I currently step down the hierarchy using the code below.<br/>
edit: I was told this can be caused by objects not being active. they looked active to me in unity explorer though. so potential fix I was told: use Resources.Find... instead?
```csharp
var screen1 =
    FindChild(
        FindChild(
            FindChild(test, "UICanvas"),
        "SafeArea"),
    "Screen1");

...

public static GameObject FindChild(GameObject parent, string name)
{
    if (parent == null)
    {
        MelonLogger.Warning("Parent GameObject is null.");
        return null;
    }

    Transform childTransform = parent.transform.Find(name);
    if (childTransform != null)
    {
        return childTransform.gameObject;
    }
    else
    {
        MelonLogger.Warning($"Child GameObject with name '{name}' not found.");
        return null; // should probably return the parent the more I think about this while writing the readme.md
    }
}
```
b) when getting objects directly using its type/class name, they don't seem to have childrens. so I currently get all objects in the scenes and filter for the ones I want like this:
```csharp
GameObject[] titleSceneObjects = GameObject.FindObjectsOfType<GameObject>();
MelonLogger.Msg($"Total objects found: {titleSceneObjects.Length}");

GameObject[] titleSceneObjects2 = Resources.FindObjectsOfTypeAll<GameObject>();
MelonLogger.Msg($"Total objects found: {titleSceneObjects2.Length}");

var test = titleSceneObjects.Where(x => x.name == "Title").FirstOrDefault();
MelonLogger.Msg($"{test}: {test.transform.childCount}");
```

## Game Scenes (spoiler):
I spotted a few gaps in between the numbering. I can't tell if this is due to cut content or other reasons.
### General:
- "Splash"
- "Title"
- "Settings"
- "PostEpisodeReport"
- "Credits"
### Episode 1:
- "E1_00_Beach"
- "E1_01_Morning"
- "E1_02_MeetTrish"
- "E1_03_Homeroom"
- "E1_04_MusicRoom"
- "E1_04A_ReedWedge"
- "E1_04B_TrishWedge"
- "E1_05_BusHome"
- "E1_06_NaserandNaomi"
- "E1_07_GroupChat"
- "E1_08_Kitchen"
- "E1_09_MeteorIntro"
- "E1_MorningMusic_MG"
- "E1_PhoneStaredown_MG"
- "E1_FangsLogoDesign_MG"
- "E1_Spices_MG"
- "E1_PerformingNewSong_MG"
- "E1_PlayForNaomi_MG"
### Episode 2:
- "E2_01_MeteorAftermath"
- "E2_02_NaserDrive"
- "E2_03_PreAssembly"
- "E2_04_EmergencyMtg"
- "E2_05_CarpeDiem"
- "E2_06_YourDiems"
- "E2_06B_NaomiWedge"
- "E2_06C_RosaWedge"
- "E2_07_MemoryBox"
- "E2_08_FangSearches"
- "E2_09A_MidiMusic"
- "E2_10_PhotoDayAM"
- "E2_11_KillMeNow"
- "E2_12_RooftopReed"
- "E2_13_NaomiTheGenius"
- "E2_14_TheWalkHome"
- "E2_15_AuditionDay_A"
- "E2_15_AuditionDay_B"
- "E2_15_AuditionDay_C"
- "E2_15_AuditionDay_D"
- "E2_MidiMusicPerf_MG"
- "E2_AuditionPerf_MG"
- "E2_Doomscroll_MG"
- "E2_AuditoriumPeopleWatching_MG"
- "E2_ControllerHunt_MG"
- "E2_FindReed_MG"
- "E2_PhotoDay_MG"
### Episode 3:
- "E3_01_CalderaDreams"
- "E3_02_BackToReality"
- "E3_04_MeteorClass"
- "E3_04B_StelleWedge"
- "E3_05_BOTBRampUp"
- "E3_06_HuntForMango"
- "E3_07_BustedForPosters"
- "E3_08_LnLIntro"
- "E3_09_LnL"
- "E3_10_BackToTheGarage"
- "E3_PosterDesign_MG"
- "E3_HuntForMango_MG"
- "E3_Books_MG"
- "E3_CrystalDoor_MG"
- "E3_SecretAdmirerLyrics_MG"
### Episode 4:
- "E4_01_CollegeApps"
- "E4_02_FutureIsSoon"
- "E4_02B_SageWedge"
- "E4_04_TimeToTry"
- "E4_05_TheTriForce"
- "E4_06_RosaRoof"
- "E4_07_TheOtherShoe"
- "E4_08_LnL2"
- "E4_09_TheShortGoodbye"
- "E4_10_BackHome"
### Episode 5:
- "E5_01_BreakfastTime"
- "E5_02_TrishWalk"
- "E5_03_TheNightBefore"
- "E5_04_TheParentCall"
- "E5_05_RideAlong"
- "E5_06_SetupTime"
- "E5_07_GreenRoom"
- "E5_07C_NaserWedge"
- "E5_08_BadVibesA"
- "E5_08B_BadVibesB"
- "E5_08C_BadVibesC"
- "E5_09_TheFight"
- "E5_10_TheAftermath"
- "E5_11_TheAurora"
- "E5_NaserPose_MG"
- "E5_SongwritingConvo_MG"
- "E5_BotBPerformance_MG"
- "E5_BotBPerformanceB_MG"
### Episode 6:
- "E6_01_ReedRooftop"
- "E6_03_BeforeLnL"
- "E6_04_LnL"
- "E6_05_AfterLnL"
- "E6_AftermathPerformance_MG"
### Episode 7:
- "E7_01_BeachAlone"
- "E7_02_FriendsArrive"
- "E7_03_TurnForWorse"
- "E7_04_Rosa"
- "E7_05_Stella"
- "E7_06_Sage"
- "E7_07_Intermission"
- "E7_08_Naser"
- "E7_09_Reed"
- "E7_10_Trish"
- "E7_11_Naomi"
- "E7_12_TheRitual"
### Episode 8:
- "E8_02_BeNotAlarmed"
- "E8_04_FarewellLavaJava"
- "E8_05_WormDramaCheckIn"
- "E8_06_NaomiDate"
- "E8_07_NaomiHang"
- "E8_08_BadNews"
- "E8_10_TrishAndFang"
- "E8_11_BeachDay"
- "E8_12_TheLastDay"
- "E8_13_OnArrival"
- "E8_13_OnArrival_Alt"
- "E8_14_FinalPrep"
- "E8_14_FinalPrep_Alt"
- "E8_15A_CalderaFest"
- "E8_15A_CalderaFest_Alt"
- "E8_15B_CalderaFest"
- "E8_15B_CalderaFest_Alt"
- "E8_15C_CalderaFest"
- "E8_15C_CalderaFest_Alt"
- "E8_Crowd_MG"
- "E8_NaomiSongwriting_MG"
- "E8_FinalPerformance_MG"
- "E8_FinalPerfomance_Alt_MG"
