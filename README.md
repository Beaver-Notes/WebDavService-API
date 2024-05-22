# WebDavService API Documentation

This API provides a set of methods to interact with a WebDAV server using React and TypeScript. The `WebDavService` class handles various WebDAV operations such as fetching files, creating folders, checking if a folder exists, and more.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Examples](#Examples)
- [Methods](#methods)
  - [constructor](#constructor)
  - [get](#get)
  - [createFolder](#createFolder)
  - [folderExists](#folderExists)
  - [propFind](#propFind)
  - [upload](#upload)
  - [getDirectoryContent](#getDirectoryContent)

## Installation

To use the `WebDavService` in your React project, install the required dependencies:

```bash
npm install axios xml2js
```
## Examples
#### Login Example
Here's how you can create an instance of the WebDavService with login credentials:

```tsx
import { WebDavService } from './path/to/webdav-service';

const options = {
  baseUrl: 'https://your-webdav-server.com',
  username: 'your-username',
  password: 'your-password',
};

const webDavService = new WebDavService(options);
console.log('Logged in to WebDAV server');
```

#### Create and Upload a Dummy File Example
This example demonstrates how to create a new folder, and upload a dummy file to that folder:

```tsx
async function createAndUploadDummyFile() {
  const options = {
    baseUrl: 'https://your-webdav-server.com',
    username: 'your-username',
    password: 'your-password',
  };

  const webDavService = new WebDavService(options);
  
  const folderPath = 'dummy-folder';
  const filePath = `${folderPath}/dummy-file.txt`;
  const fileContent = 'This is a dummy file content';

  // Create a new folder
  await webDavService.createFolder(folderPath);
  console.log(`Created folder: ${folderPath}`);

  // Upload a dummy file to the new folder
  await webDavService.upload(filePath, fileContent);
  console.log(`Uploaded file: ${filePath}`);
}

createAndUploadDummyFile();
```
## Usage

First, import the `WebDavService` class and create an instance with the necessary options:

```tsx
import { WebDavService } from './path/to/webdav-service';

const options = {
  baseUrl: 'https://your-webdav-server.com',
  username: 'your-username',
  password: 'your-password',
};

const webDavService = new WebDavService(options);
```

## Methods

### constructor

Creates an instance of the `WebDavService` class.

```tsx
constructor(options: WebDavOptions)
```

#### Parameters

- `options` (WebDavOptions): An object containing the base URL, username, and password for the WebDAV server.

### get

Fetches a file from the WebDAV server.

```tsx
async get(path: string): Promise<string>
```

#### Parameters

- `path` (string): The path to the file on the WebDAV server.

#### Returns

- `Promise<string>`: The content of the file.

#### Example

```tsx
const fileContent = await webDavService.get('path/to/file.txt');
console.log(fileContent);
```

### createFolder

Creates a new folder on the WebDAV server.

```tsx
async createFolder(folderPath: string): Promise<void>
```

#### Parameters

- `folderPath` (string): The path where the new folder should be created.

#### Example

```tsx
await webDavService.createFolder('path/to/new-folder');
```

### folderExists

Checks if a folder exists on the WebDAV server.

```tsx
async folderExists(path: string): Promise<boolean>
```

#### Parameters

- `path` (string): The path to the folder.

#### Returns

- `Promise<boolean>`: `true` if the folder exists, `false` otherwise.

#### Example

```tsx
const exists = await webDavService.folderExists('path/to/folder');
console.log(exists); // true or false
```

### propFind

Performs a PROPFIND request to get properties of a resource on the WebDAV server.

```tsx
async propFind(path: string, depth: number = 1): Promise<any>
```

#### Parameters

- `path` (string): The path to the resource.
- `depth` (number): The depth of the PROPFIND request (default is 1).

#### Returns

- `Promise<any>`: The parsed XML response.

#### Example

```tsx
const properties = await webDavService.propFind('path/to/resource');
console.log(properties);
```

### upload

Uploads a file to the WebDAV server.

```tsx
async upload(filePath: string, content: string | Blob): Promise<void>
```

#### Parameters

- `filePath` (string): The path where the file should be uploaded.
- `content` (string | Blob): The content of the file.

#### Example

```tsx
const fileContent = 'Hello, world!';
await webDavService.upload('path/to/upload.txt', fileContent);
```

### getDirectoryContent

Gets the content of a directory on the WebDAV server.

```tsx
async getDirectoryContent(path: string): Promise<any>
```

#### Parameters

- `path` (string): The path to the directory.

#### Returns

- `Promise<any>`: The raw XML response.

#### Example

```tsx
const directoryContent = await webDavService.getDirectoryContent('path/to/directory');
console.log(directoryContent);
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
