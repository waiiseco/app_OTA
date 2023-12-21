# New OTA update

First of all, you should build the app in prod mode:

```jsx
ionic capacitor build ios --prod --no-open
```

Then, generate the zip file:

```jsx
npx @capgo/cli bundle zip --path www/ --bundle [ota_version_number]
```
This will generate a .zip file that we need to encrypt:

```jsx
npx @capgo/cli bundle encrypt [path/to/zip]
```

This will generate a file .zip_encrypted.zip and a key.

We upload the file to the root of this repository, and will edit the versions.json file:
- Add a new entry in the "app_versions" whit the format: 
```
{
  "app_version_number": "ota_version_number"
}
```
- Add a new entry in the "session_keys" with the format:
```
{
  "version_number": "key"
}
```

After doing this, when the user opens the app, the new version will be downloaded and applied on the next restart of the app