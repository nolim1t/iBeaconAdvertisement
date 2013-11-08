iBeaconAdvertisement
====================

Helper class to help turn your Mac into an iBeacon (this is so much better than an iOS device)


Code
--------------

1. Copy these two classes into your Mac project
2. Libraries required: IOBluetooth
3. Add the following code somewhere (such as your app delegate?) to implement the correct delegates
 
```objc
@interface ViewControllerOrAppDelegate () <CBPeripheralManagerDelegate>
@property (nonatomic,strong) CBPeripheralManager *manager;
@end

```

Add  in the following method
```objc
- (void)peripheralManagerDidUpdateState:(CBPeripheralManager *)peripheral {
    
    if (peripheral.state == CBPeripheralManagerStatePoweredOn) {
        
        NSUUID *proximityUUID = [[NSUUID alloc] initWithUUIDString:@"E2C56DB5-DFFB-48D2-B060-D0F5A71096E0"];
        
        BeaconAdvertisementUtil *beaconData = [[BeaconAdvertisementUtil alloc] initWithProximityUUID:proximityUUID
                                                                                                     major:5
                                                                                                     minor:5000
                                                                                             measuredPower:-59];
        
        
        [_manager startAdvertising:beaconData.beaconAdvertisement];
    }
}
```

Where you want to start the broadcast, add in the following

```objc
 _manager = [[CBPeripheralManager alloc] initWithDelegate:self
                                                       queue:nil];

```

