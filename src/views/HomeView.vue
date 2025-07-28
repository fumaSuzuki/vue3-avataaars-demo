<script setup>
import { ref, computed } from 'vue'
import { Avatar, Factory } from 'vue3-avataaars'

// --- アバターパーツの利用可能なオプションを定義 ---
// https://github.com/n1c/vue3-avataaars/blob/main/src/config/options.ts から取得した全オプション
const topTypeOptions = [
  'NoHair',
  'Eyepatch',
  'Hat',
  'Hijab',
  'Turban',
  'WinterHat1',
  'WinterHat2',
  'WinterHat3',
  'WinterHat4',
  'LongHairBigHair',
  'LongHairBob',
  'LongHairBun',
  'LongHairCurly',
  'LongHairCurvy',
  'LongHairDreads',
  'LongHairFrida',
  'LongHairFro',
  'LongHairNotTooLong',
  'LongHairMiaWallace',
  'LongHairStraight',
  'LongHairStraight2',
  'LongHairStraightStrand',
  'ShortHairDreads01',
  'ShortHairDreads02',
  'ShortHairFrizzle',
  'ShortHairShaggyMullet',
  'ShortHairShortCurly',
  'ShortHairShortFlat',
  'ShortHairShortRound',
  'ShortHairShortWaved',
  'ShortHairSides',
  'ShortHairTheCaesar',
  'ShortHairTheCaesarAndSidePart',
]

const accessoriesTypeOptions = ['Blank', 'PrescriptionGlasses', 'Sunglasses', 'Wayfarers']

const hairColorOptions = [
  'Auburn',
  'Black',
  'Blonde',
  'BlondeGolden',
  'Brown',
  'BrownDark',
  'PastelPink',
  'Platinum',
  'Red',
  'SilverGray',
]

const facialHairTypeOptions = [
  'Blank',
  'BeardMedium',
  'BeardLight',
  'BeardMajestic',
  'MoustacheFancy',
  'MoustacheMagnum',
]

const facialHairColorOptions = [
  'Auburn',
  'Black',
  'Blonde',
  'BlondeGolden',
  'Brown',
  'BrownDark',
  'PastelPink',
  'Platinum',
  'Red',
  'SilverGray',
]

const clotheTypeOptions = [
  'BlazerShirt',
  'BlazerSweater',
  'CollarSweater',
  'GraphicShirt',
  'Hoodie',
  'Overall',
  'ShirtCrewNeck',
  'ShirtScoopNeck',
  'ShirtVNeck',
]

const clotheColorOptions = [
  'Black',
  'Blue01',
  'Blue02',
  'Blue03',
  'Gray01',
  'Gray02',
  'Heather',
  'PastelBlue',
  'PastelGreen',
  'PastelOrange',
  'PastelRed',
  'PastelYellow',
  'Pink',
  'Red',
  'White',
]

const eyeTypeOptions = [
  'Close',
  'Cry',
  'Default',
  'Dizzy',
  'EyeRoll',
  'Happy',
  'Hearts',
  'Side',
  'Squint',
  'Surprised',
  'Wink',
  'WinkWacky',
]

const eyebrowTypeOptions = [
  'Angry',
  'AngryNatural',
  'Default',
  'DefaultNatural',
  'FlatNatural',
  'FrownNatural',
  'RaisedExcited',
  'RaisedExcitedNatural',
  'SadConcerned',
  'SadConcernedNatural',
  'UnibrowNatural',
  'UpDown',
  'UpDownNatural',
]

const mouthTypeOptions = [
  'Concerned',
  'Default',
  'Disbelief',
  'Eating',
  'Grimace',
  'Sad',
  'Smile',
  'ScreamOpen',
  'Tongue',
  'Twinkle',
  'Vomit',
]

const skinColorOptions = ['Tanned', 'Yellow', 'Pale', 'Light', 'Brown', 'DarkBrown', 'Black']

const graphicTypeOptions = [
  'Bat',
  'Bear',
  'Cumbia',
  'Deer',
  'Diamond',
  'Hola',
  'Laura',
  'Pizza',
  'Resist',
  'Selena',
  'Deer',
]

// --- ユーザーの選択を保持するリアクティブな変数 (初期値設定) ---
// Factory({}) でランダムに初期値を設定し、UIとアバターの表示を同期させます。
const initialAvatarProps = Factory({}) // 最初にランダムなプロパティセットを生成

const selectedTopType = ref(initialAvatarProps.topType || topTypeOptions[0])
const selectedAccessoriesType = ref(initialAvatarProps.accessoriesType || accessoriesTypeOptions[0])
const selectedHairColor = ref(initialAvatarProps.hairColor || hairColorOptions[0])
const selectedFacialHairType = ref(initialAvatarProps.facialHairType || facialHairTypeOptions[0])
const selectedFacialHairColor = ref(initialAvatarProps.facialHairColor || facialHairColorOptions[0])
const selectedClotheType = ref(initialAvatarProps.clotheType || clotheTypeOptions[0])
const selectedClotheColor = ref(initialAvatarProps.clotheColor || clotheColorOptions[0])
const selectedEyeType = ref(initialAvatarProps.eyeType || eyeTypeOptions[0])
const selectedEyebrowType = ref(initialAvatarProps.eyebrowType || eyebrowTypeOptions[0])
const selectedMouthType = ref(initialAvatarProps.mouthType || mouthTypeOptions[0])
const selectedSkinColor = ref(initialAvatarProps.skinColor || skinColorOptions[0])
const selectedGraphicType = ref(initialAvatarProps.graphicType || 'None') // 'None' はグラフィックなし、またはFactory任せを意図

// --- アバターのプロパティを動的に生成するComputedプロパティ ---
// Factoryが生成する完全なプロパティをベースに、ユーザーの選択で上書きします。
const dynamicAvatarProps = computed(() => {
  // まず、Factoryでアバターの全てのプロパティ（背景、姿勢などを含む）を生成
  // これがアバター描画の「土台」になります。
  const baseProps = Factory({})

  // その土台のプロパティをスプレッド構文で展開し、
  // ユーザーが選択した個別のプロパティで上書きします。
  const finalProps = {
    ...baseProps,
    topType: selectedTopType.value,
    accessoriesType: selectedAccessoriesType.value,
    hairColor: selectedHairColor.value,
    facialHairType: selectedFacialHairType.value,
    facialHairColor: selectedFacialHairColor.value,
    clotheType: selectedClotheType.value,
    clotheColor: selectedClotheColor.value,
    eyeType: selectedEyeType.value,
    eyebrowType: selectedEyebrowType.value,
    mouthType: selectedMouthType.value,
    skinColor: selectedSkinColor.value,
  }

  // graphicType は 'None' が選択された場合、baseProps.graphicType (ランダムな値かundefined) を利用
  // それ以外の場合は selectedGraphicType.value を利用
  // これにより、UIで「（ランダム/デフォルト）」を選んだらランダムなグラフィックに、
  // 特定のグラフィックを選んだらそれが適用されるようになります。
  if (selectedGraphicType.value !== 'None') {
    finalProps.graphicType = selectedGraphicType.value
  } else {
    // Factoryが生成するrandomProps.graphicTypeがnull/undefinedの場合に備え、
    // ここでdeleteする必要はありません。basePropsがすでに適切な値を保持しています。
    // 明示的にgraphicTypeを持たせたくない場合は、Factoryがデフォルトで割り当てる
    // graphicTypeをnullやundefinedに上書きすればよいですが、
    // 今回は「（ランダム/デフォルト）」なので、Factory任せの挙動でOKです。
  }

  return finalProps
})

// --- ランダムなアバターを生成する関数 ---
const generateRandomAvatar = () => {
  const randomProps = Factory({}) // 全てランダムに生成

  // 生成されたランダムな値を各selected変数に代入し、UIを更新
  selectedTopType.value = randomProps.topType || topTypeOptions[0]
  selectedAccessoriesType.value = randomProps.accessoriesType || accessoriesTypeOptions[0]
  selectedHairColor.value = randomProps.hairColor || hairColorOptions[0]
  selectedFacialHairType.value = randomProps.facialHairType || facialHairTypeOptions[0]
  selectedFacialHairColor.value = randomProps.facialHairColor || facialHairColorOptions[0]
  selectedClotheType.value = randomProps.clotheType || clotheTypeOptions[0]
  selectedClotheColor.value = randomProps.clotheColor || clotheColorOptions[0]
  selectedEyeType.value = randomProps.eyeType || eyeTypeOptions[0]
  selectedEyebrowType.value = randomProps.eyebrowType || eyebrowTypeOptions[0]
  selectedMouthType.value = randomProps.mouthType || mouthTypeOptions[0]
  selectedSkinColor.value = randomProps.skinColor || skinColorOptions[0]
  selectedGraphicType.value = randomProps.graphicType || 'None'
}
</script>

<template>
  <div class="container">
    <h1 class="title">
      <span class="text-blue">アバター</span>を<span class="text-green">カスタマイズ</span>しよう！
    </h1>

    <div class="grid-layout">
      <div class="controls-panel">
        <h2 class="section-title">パーツを選ぼう</h2>

        <div class="control-group">
          <label for="topType" class="label">髪型:</label>
          <select id="topType" v-model="selectedTopType" class="select-input">
            <option v-for="option in topTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="hairColor" class="label">髪色:</label>
          <select id="hairColor" v-model="selectedHairColor" class="select-input">
            <option v-for="option in hairColorOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="eyeType" class="label">目の形:</label>
          <select id="eyeType" v-model="selectedEyeType" class="select-input">
            <option v-for="option in eyeTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="eyebrowType" class="label">眉毛の形:</label>
          <select id="eyebrowType" v-model="selectedEyebrowType" class="select-input">
            <option v-for="option in eyebrowTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="mouthType" class="label">口の形:</label>
          <select id="mouthType" v-model="selectedMouthType" class="select-input">
            <option v-for="option in mouthTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="skinColor" class="label">肌の色:</label>
          <select id="skinColor" v-model="selectedSkinColor" class="select-input">
            <option v-for="option in skinColorOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="facialHairType" class="label">ひげの種類:</label>
          <select id="facialHairType" v-model="selectedFacialHairType" class="select-input">
            <option v-for="option in facialHairTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="facialHairColor" class="label">ひげの色:</label>
          <select id="facialHairColor" v-model="selectedFacialHairColor" class="select-input">
            <option v-for="option in facialHairColorOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="clotheType" class="label">服の種類:</label>
          <select id="clotheType" v-model="selectedClotheType" class="select-input">
            <option v-for="option in clotheTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="clotheColor" class="label">服の色:</label>
          <select id="clotheColor" v-model="selectedClotheColor" class="select-input">
            <option v-for="option in clotheColorOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="graphicType" class="label">服のグラフィック:</label>
          <select id="graphicType" v-model="selectedGraphicType" class="select-input">
            <option value="None">（ランダム/デフォルト）</option>
            <option v-for="option in graphicTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <div class="control-group">
          <label for="accessoriesType" class="label">メガネ:</label>
          <select id="accessoriesType" v-model="selectedAccessoriesType" class="select-input">
            <option v-for="option in accessoriesTypeOptions" :key="option" :value="option">
              {{ option }}
            </option>
          </select>
        </div>

        <button @click="generateRandomAvatar" class="random-button">ランダム生成！</button>
      </div>

      <div class="avatar-display">
        <Avatar v-bind="dynamicAvatarProps" :size="300" />
      </div>
    </div>
  </div>
</template>

<style scoped>
/* フォントのインポート */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

body {
  font-family: 'Inter', sans-serif;
  background-color: #f3f4f6;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 1.5rem;
  background-color: #ffffff;
  border-radius: 0.75rem; /* rounded-xl */
  box-shadow:
    0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05); /* shadow-lg */
}

.title {
  font-size: 2.25rem; /* text-4xl */
  font-weight: 800; /* font-extrabold */
  text-align: center;
  color: #1f2937; /* text-gray-800 */
  margin-bottom: 2.5rem; /* mb-10 */
  line-height: 1.2;
}

.text-blue {
  color: #2563eb; /* text-blue-600 */
}

.text-green {
  color: #16a34a; /* text-green-600 */
}

.grid-layout {
  display: grid;
  grid-template-columns: 1fr; /* mobile: 1 column */
  gap: 3rem; /* gap-12 */
  align-items: flex-start; /* items-start */
}

@media (min-width: 768px) {
  /* md: */
  .grid-layout {
    grid-template-columns: 1fr 1fr; /* md: grid-cols-2 */
  }
}

.controls-panel {
  display: flex;
  flex-direction: column;
  gap: 1.5rem; /* space-y-6 */
  background-color: #f9fafb; /* bg-gray-50 */
  padding: 1.5rem; /* p-6 */
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.06); /* shadow-inner */
}

.section-title {
  font-size: 1.5rem; /* text-2xl */
  font-weight: 700; /* font-bold */
  color: #374151; /* text-gray-700 */
  margin-bottom: 1rem; /* mb-4 */
}

.control-group {
  margin-bottom: 1rem; /* 各コントロールグループ間の間隔 */
}

.label {
  display: block;
  font-size: 1.25rem; /* text-xl */
  font-weight: 500; /* font-medium */
  color: #374151; /* text-gray-700 */
  margin-bottom: 0.5rem; /* mb-2 */
}

.select-input {
  display: block;
  width: 100%;
  padding: 0.75rem 2.5rem 0.75rem 0.75rem; /* pl-3 pr-10 py-3 */
  font-size: 1.125rem; /* sm:text-lg, base:text-base */
  border: 1px solid #d1d5db; /* border-gray-300 */
  border-radius: 0.375rem; /* rounded-md */
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
  outline: none; /* focus:outline-none */
  -webkit-appearance: none; /* デフォルトの矢印を非表示に */
  -moz-appearance: none;
  appearance: none;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 20 20' fill='none'%3e%3cpath d='M7 7l3 3 3-3m0 6l-3-3-3 3' stroke='%239CA3AF' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3e%3c/svg%3e");
  background-repeat: no-repeat;
  background-position: right 0.75rem center;
  background-size: 1.5em 1.5em;
  transition:
    border-color 0.15s ease-in-out,
    box-shadow 0.15s ease-in-out;
}

.select-input:focus {
  border-color: #3b82f6; /* focus:border-blue-500 */
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.25); /* focus:ring-blue-500 */
}

.random-button {
  width: 100%;
  background-color: #9333ea; /* bg-purple-600 */
  color: #ffffff; /* text-white */
  font-weight: 700; /* font-bold */
  padding: 0.75rem 1.5rem; /* py-3 px-6 */
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow:
    0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06); /* shadow-lg */
  transition:
    background-color 0.3s ease-in-out,
    transform 0.3s ease-in-out; /* transition duration-300 ease-in-out */
  font-size: 1.25rem; /* text-xl */
  cursor: pointer;
  border: none;
}

.random-button:hover {
  background-color: #7e22ce; /* hover:bg-purple-700 */
  transform: scale(1.02); /* hover:scale-105 を少し抑えた */
}

.avatar-display {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #ffffff; /* bg-white */
  padding: 1.5rem; /* p-6 */
  border-radius: 0.5rem; /* rounded-lg */
  box-shadow:
    0 4px 6px -1px rgba(0, 0, 0, 0.1),
    0 2px 4px -1px rgba(0, 0, 0, 0.06); /* shadow-md */
  border: 2px dashed #e5e7eb; /* border-2 border-dashed border-gray-200 */
  min-height: 400px;
}
</style>
