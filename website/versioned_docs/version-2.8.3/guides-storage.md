---
id: version-2.8.3-guides-storage
title: Storage
sidebar_label: Storage
original_id: guides-storage
---

Canner provides different storages for you to customize where to store files of your CMS.

> Currently, files are not from your local server, storage features are supported cloud services data.

## Usage

New the storage instances, and put them into `imageStorage` or `fileStorage` properties of any data tags. Storage instance must be an object generated from [@canner/storage]( https://github.com/Canner/canner/blob/canary/packages/canner-storage/src/index.js).

> You don't have to install `@canner/storage` manually because it's a dependency of canner

```jsx
import CannerScript from 'canner-script';
import {FirebaseClientStorage, ImgurStorage} from '@canner/storage';
...
const fileStorage = new FirebaseClientStorage(options);
const imageStorage = new ImgurStorage(options);

export default (
  <root fileStorage={fileStorage} imageStorage={imageStorage}>
  ...
  </root>
)
```

## Storage List

- ImgurStorage
- FirebaseClientStorage

### ImgurStorage

Upload image to [Imgur](https://imgur.com/).

```js
import {ImgurStorage} from '@canner/storage';

const imageStorage = new ImgurStorage({
  clientId, // https://apidocs.imgur.com/
  mashapeKey // https://market.mashape.com/imgur/imgur-9#image-upload
});


export default (
  <root>
    <object
      keyName="overview"
      title="Overview Tab"
      imageStorage={imageStorage} // -------> your storage settings
      connector={connector}
      resolver={resolver}>
      <string title="Your name" keyName="name"/>
    </object>
  </root>
)
```

### FirebaseClientStorage

Enable Firebase storage to store your files, you can new a `FirebaseClientStorage` instance and pass to prop `fileStorage` into `<Canner>` component.

```js
import CannerScript from 'canner-script';
import {FirebaseClientStorage} from '@canner/storage';
import firebase from 'firebase';

firebase.initializeApp({
  apiKey,
  storageBucket
});

// remember to authenticate firebase first, or uploading will be failed,
// https://firebase.google.com/docs/auth/web/start
firebase.auth().signInAnonymously();
// or login your firebase Auth
firebase.auth().signInWithEmailAndPassword("xxx", "xxx");

const fileStorage = new FirebaseClientStorage({firebase});

export default (
  <root>
    <object
      keyName="overview"
      title="Overview Tab"
      fileStorage={fileStorage} // -------> your storage settings
      connector={connector}
      resolver={resolver}>
      <string title="Your name" keyName="name"/>
    </object>
  </root>
)
```