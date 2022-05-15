# Erka React Bootcamp Notları

- React'ın ortaya çıkmasındaki ana nedenlerden biri sayfada sürekli render edilmesi gereken alanlar varsa komple bütün sayfayı render etmek yerine ilgili alanların render edilmesini sağlamaktı.

- Bu şekillde React tekrar tekrar render edilme problemini de çözmüş oluyor.

- Paint Flashing açmak;
    ```
    Chrome Dev Tools > Üç Nokta > More Tools > Rendering > Paint flashing
    ```

- React, Angular gibi frameworklerden farklı olarak sadece View katmanına yönelmiş, View katmanındaki performans problemlerini gidermeyi amaçlamıştır.

- Sayfa yüklendikten sonra bundle.js id'si "root" olan div'i dolduruyor.

- Bir modül birden fazla export yapabilir, yalnız bir adet default export yapabilir.

- Component isimleri büyük harfle başlamalı.

- Özel tanımlı JavaScript keywordlerini JSX içindeki HTML'de **kullanamayız**.
    ```html
    <div class="class-adi"> yerine <div className="class-adi"> yazmalıyız.
    ```

- Koşullu bir işlem yaparken;
    ```javascript
    {data ? xxx : xxx} ve ya {data && xxx} gibi koşul yazabiliriz.
    ```

- Destructing yaparken; objelerde ve fonksiyonlarda keyler **aynı** olmak zorunda. Arraylerde ise destructing **index numarası**na göre yapılır.

- Ortam değişkenlerini projeye çekerken başına **REACT_APP** prefixini eklemeliyiz.

---

## Props
- Propslara string dışı ifade yollayacaksak süslü parantez ile sarmalıyız.
    ```html
    <ComponentName value={xxx} />
    ```

- Proplara tip doğrulamasını [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html) ile yapabiliriz. Dilersek varsayılan prop değeri de geçebiliriz.
    ```javascript
    Paragraph.propTypes = {
        text: PropTypes.string,
        age: PropTypes.number,
        user: PropTypes.exact({
            name: PropTypes.string,
            surname: PropTypes.string,
        })
    }

    Paragraph.defaultProps = {
        text: "Varsayılan paragraf",
    }
    ```

---

## State
- Statelerde değer değiştirirken prev state'i almak önem taşır.
    ```javascript
    setCount((prev) => prev - 1);
    ```

---

## Lifecycle
- useEffect hook'u parametre olarak callback ve dependency alır. Ayrıca birden fazla dependencyde verebiliriz.
    ```javascript
    useEffect((callback) => {
        console.log(xxx);
    }, [dependency1, dependency2]);
    ```

- Component mount olduğu anda çalışır

- Eğer bir dependecy vermezsek, herbir state değiştiğinde tekrarlanır.

- useEffect mutlaka birinci seviyede olmak zorunda. Yani herhangi bir if kontrolü içinde olamaz.

- useEffect'in return'unde component unmount anını yakalayabiliriz.

- Component mount olduğunda çalıştığı için fetch işlemlerini'de useEffect içinde yapabiliriz. fetch yaparken [axios](https://www.npmjs.com/package/axios) kullanabiliriz.
    ```javascript
    useEffect(() => {
        fetch(url)
            .then(res => res.json())
            .then(data => console.log(data));
    }, [])

    /* veya */

    useEffect(() => {
        axios(url)
            .then(res => console.log(res.data))
    }, [])
    ```

    - Kendi asenkron fonksiyonlarımızı da yazabiliriz. Örnek fonksiyona [Codesandbox](https://codesandbox.io/s/vigorous-silence-vnjqlx?file=/src/components/Users.js) linkinden bakabilirsiniz.

- [React.memo](https://tr.reactjs.org/docs/react-api.html#reactmemo): Göndermiş olduğumuz parametreleri öncekilerle karşılaştırıp gereksiz render etmez.
    - Farklı bir component'de işlem yaparken [useMemo](https://tr.reactjs.org/docs/hooks-reference.html#usememo) kullansak bile ilgili componenti export ederken React.memo ile sarmalıyız.
        ```javascript
        function MyComponent(props) {
        /* prop'ları kullanarak render et */
        }
        function areEqual(prevProps, nextProps) {
        /*
        nextProps'u render'a iletmek,
        prevProps'u render'a iletmek ile aynı sonucu verirse true
        aksi takdirde false döndürür
        */
        }
        export default React.memo(MyComponent, areEqual);
        ```

    - Fonksiyonlar için [useCallback](https://tr.reactjs.org/docs/hooks-reference.html#usecallback) kullanmalıyız, ilgili componentin yine React.memo ile sarmalanmış olması gerek.

---

## React Router
- root render edilirken componentleri BrowserDefault ile sarmalıyız.

---

## Form Validasyon
- [Formik](https://formik.org/) aracını kullanıyoruz.

- [yup](https://github.com/jquense/yup) şeması ile Formikteki keyler eşleşmeli.

---

## Context API
- Provider kelimesini veri sağlayıcı anlamında literatürümüze alabiliriz.

---

## React Developer Olma Yolunda Öğrenmen veya Göz Atman Gerekenler
- Test yazmak,

- Uygulamanı deploy etmek,

- Localization,

- Paket yazmak ve npm'de paylaşmak,

- [Recoil - A state management library for React](https://recoiljs.org/)

- [Jotai - Primitive and flexible state management for React](https://jotai.org/)

- [Zustand - A small, fast and scalable bearbones state-management solution using simplified flux principles.](https://github.com/pmndrs/zustand)

- [Redux - A Predictable State Container for JS Apps](https://redux.js.org/)

- [Redux Toolkit - The official, opinionated, batteries-included toolset for efficient Redux development](https://redux-toolkit.js.org/)

- [React Query - Performant and powerful data synchronization for React](https://react-query.tanstack.com/)

- [Remix](https://remix.run/)

- [styled-components](https://styled-components.com/)

Youtube kanalları;
- [Rocketseat](https://www.youtube.com/c/RocketSeat)

- [Ben Awad](https://www.youtube.com/c/BenAwad97)

Visual Studio Code eklentileri;
- [ES7+ React/Redux/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets)

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)