# 🎧 Lisn Kids - React Native Application

####  👋🏼 Welcome to the portfolio dedicated to the Lisn Kids project - 👀 __Ask me to look at all the code__
I personally and mainly worked on the player audio. Then you can add a playlist and custom it as you want, and lisn't  all song with the Night Mode Protected or just classic. 
> More explications lower... 👇

**Enjoy !** 
 


![LisnKids01](/assets/img/presentation.gif)
## For who and for what ?

🏋🏼‍♂️ I worked with 4 people in 2 weeks for [Angelina Sirba](https://www.linkedin.com/in/angeline-sirba-b8b242150/), the official CEO of [Lisn Kids](https://www.instagram.com/lisnkids_fr/) and [Boobox](https://www.boobox.io/), a famous website for read a lot of digital books.

👶🏼 The goal was to create an **audible application** for children, with many features, and we didn't know if we could do everything in the allotted time...
 
![LisnKids02](/assets/img/02.png)

## Player Audio Extract 🎧

I used [expo-av](https://docs.expo.io/versions/latest/sdk/av/) to work on the player audio.

### 1. Read all episode in a serie
![Gif01](/assets/img/playeraudio-serie.gif)

extract code with expo-av : 
![CodeCarbon](/assets/img/carbon01.png)

With NewRank's State, we can doing next or previous
```javascript
const togglePrevious = () => {
    if (sound) {
      sound.unloadAsync();
      setPlayingStatus("nosound");
    }
    const newRank = rankSong - 1;
    setRankSong(newRank);
    setCurrentSoundData(data[newRank - 1]);
  };
```

### 2. Then you can add somes episodes in your playlist 
... and the `data` change if you play all the songs of your playlist. We use the same audio player than the previous gif 😄
![Gif02](/assets/img/playlist.gif)
```javascript
<AntDesign 
  name="plus" 
  size={40}         
  onPress={() => {
    handleAddPlaylistEpisode(item._id);
  }}
/>
```

```javascript
const handleAddPlaylistEpisode = async (idEpisode) => {
  try {
    const formData = new FormData();
    const childrenInfos = await AsyncStorage.getItem("childrenInfos");
    const children = JSON.parse(childrenInfos);

    formData.append("idChildren", children._id);
    formData.append("idEpisode", idEpisode);

    const res = await axios.post(
      `https://our-api.herokuapp.com/addEpisodeMyplaylists`,
      formData,
      {
        headers: {
          Authorization: "Bearer Token",
          "Content-Type": "multipart/form-data",
        },
      }
    );
    if (res.data) {
      setChildrenInfosStorage(res.data);
      setAddPlaylist(res.data);
    } else {
      setError("Une erreur s'est produite. Veuillez réessayer");
    }
  } catch (error) {
    console.log(error);
  }
};
```

### 3. With your playlist you can go in the night mode protected
And your children isn't attracted by the phone, and can't use it. 🛌💤
You need parental code in the switch for going back !
![Gif03](/assets/img/nightmodeprotected.gif)

## Sign In / Sign Up & Guidance 🙋📜
![Gif04](/assets/img/signin-up.gif)

## Add your children 👶
![Gif05](/assets/img/addchildren.gif)

## Switch in a parent mode for more settings and sign out ✖️👋
![Gif06](/assets/img/deconnexion.gif)

## Thanks a lot to...
![LisnKids08](/assets/img/08.png)
