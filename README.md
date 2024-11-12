## Google API

### 1. GoogleApi

- The `GoogleApi` class provides methods to create authenticated Google Drive and Google Sheets API clients. 
- It supports both OAuth2 and Service Account authorization, automatically determining the correct authorization type based on the credentials file provided.
#### Methods
- **`getDriveService(String credentialsPath)`**: Creates and returns an authenticated Google Drive client.
- **`getSheetsService(String credentialsPath)`**: Creates and returns an authenticated Google Sheets client.

**Usage Example**:
```java
Drive driveService = GoogleApi.getDriveService("path/to/credentials.json");
Sheets sheetsService = GoogleApi.getSheetsService("path/to/credentials.json");
```

### 2. GoogleDriveApi
`GoogleDriveApi` provides methods to interact with Google Drive, such as checking for folder existence, creating folders, uploading files, moving files, and retrieving folder IDs.

**Usage Example**:
```java
GoogleDriveApi driveApi = new GoogleDriveApi("path/to/credentials.json");
driveApi.createFolder("New folder");
```

### 3. GoogleSheetApi
`GoogleSheetApi` provides methods to interact with Google Sheet, such as creating spreadsheets, reading and updating cell values, freezing rows, managing sheet properties, and downloading sheet data.

**Usage Example**:
```java
GoogleSheetApi sheetApi = new GoogleSheetApi("path/to/credentials.json");
sheetApi.createSpreadSheet("New Sheet");
```
## Implement Singleton instance

### 1. DriveService
```
public class DriveService extends GoogleDriveApi {
    private DriveService(String credentialsPath) {
        super(credentialsPath);
    }
    private static volatile DriveService instance;
    public static DriveService getInstance() {
        DriveService localInstance = instance;
        if (localInstance == null) {
            synchronized (DriveService.class) {
                localInstance = instance;
                if (localInstance == null) {
                    String credentialsPath = "path/to/credentials.json";
                    instance = localInstance = new DriveService(credentialsPath);
                }
            }
        }
        return localInstance;
    }
}
```

**Usage Example**:
```java
DriveService driveService = DriveService.getInstance();
driveService.createFolder("New folder");
```

### 2. SheetService
```
public class SheetService extends GoogleSheetApi {

    private SheetService(String credentialsPath) {
        super(credentialsPath);
    }

    private static volatile SheetService instance;

    public static SheetService getInstance() {
        SheetService localInstance = instance;
        if (localInstance == null) {
            synchronized (SheetService.class) {
                localInstance = instance;
                if (localInstance == null) {
                    String credentialsPath =  "path/to/credentials.json";
                    instance = localInstance = new SheetService(credentialsPath);
                }
            }
        }
        return localInstance;
    }
}
```

**Usage Example**:
```java
SheetService sheetService = SheetService.getInstance();
sheetService.createSpreadSheet("New Sheet");
```
