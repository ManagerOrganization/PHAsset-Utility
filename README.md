A category to simplify a few tasks for the PHAsset class. 

This class assumes that you've already prompted for permissions like so:

```
[PHPhotoLibrary requestAuthorization:^(PHAuthorizationStatus status) {
    // This has happened
}];
```

Sample: Save a UIImage to camera roll (returns PHAsset in completion block)

```
UIImage *image = [UIImage imageNamed:@"terribleImage"];
[PHAsset saveImageToCameraRoll:image 
                      location:nil 
               completionBlock:^(PHAsset *asset, BOOL success) {
                   NSLog(@"asset saved to camera roll");
               }];
```

Save video (from NSURL) to camera roll (returns PHAsset in completion block)

```
NSURL *url = [NSURL urlWithString:@"terribleURL"];
[PHAsset saveVideoAtURL:videoFileURL 
               location:nil 
        completionBlock:^(PHAsset *asset, BOOL success) {
            NSLog(@"asset saved to camera roll");
        }];
```


Sample usage for saving an PHAsset to an album (will create the album if it doesn't exist):

```
PHAsset *asset = // however you are getting your PHAsset
[asset saveToAlbum:@"My App Album" completionBlock:^(BOOL success) {
    if(success){
        // Your asset now resides in My App Album
    } else {
        // Something bad happened. Handle it here.
    }
}];
```

Sample usage for getting metadata from a PHAsset

```
PHAsset *asset = // however you are getting your PHAsset
[asset requestMetadataWithCompletionBlock:^(NSDictionary *metadata) {
    NSLog(@"Metadata: %@", metadata);
}];
```

Sample use for updating or assigning a location to an asset

```
CLLocation *location = [[CLLocation alloc]initWithLatitude:37.5 longitude:-122];
NSDate *date = [NSDate date];
[asset updateLocation:location creationDate:date completionBlock:^(BOOL success) {
    if(success){
        // Asset has new location and date
    } else {
        // Something bad happened. Handle it here.
    }
}];
```


