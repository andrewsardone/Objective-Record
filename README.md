## Intro
This is a lightweight ActiveRecord way of managing Core Data objects.
The syntax is borrowed from Ruby on Rails.
And yeah, no AppDelegate code.

### Usage
1. Clone the repository in your project, and add it to the XCode
2. #import "ObjectiveRecord.h" in your model or .pch file.

#### CocoaPods
Coming soon.

### Example
``` objc

Person *john = [Person create];
john.name = @"John";
john.save;

Person *john = [Person where:@"name == 'John'"].first;
john.delete;

for(Person *person in [Person all]) {
  NSLog(@"Person: %@", person);
}
```
With new Objective-C literals, you'll be able to do:
``` objc
NSArray *people = [Person where:@{ @"age" : @18 }];

NSArray *people = [Person where:@{ @"age" : @18,
                  @"member" : @YES,
                  @"state" : @"NY"
                  }];

Person *john = [Person create:@{ @"name" : @"John", @"age" : @12, @"member" : @NO }];
```
<br><br>

### Custom ManagedObjectContext
You can also use your own ManagedObjectContext while fetching.
This is great if you have to do lots of changes, but don't want to notify anyone observing the default context until all the changes are made.
``` objc
NSManagedObjectContext *newContext = [NSManagedObjectContext new];

Person *john = [Person createInContext:newContext];
Person *john = [Person where:@"name == 'John'" inContext:newContext].first;
NSArray *people = [Person allInContext:newContext];
```

### Custom CoreData model or .sqlite database
If you've added the Core Data manually, you can change the custom model and database name in CoreDataManager.m
``` objc

static NSString *CUSTOM_MODEL_NAME = @"Database";
static NSString *CUSTOM_DATABASE_NAME = nil;
```

####ToDo
Try to make ```where:(NSString *)condition``` take va_args like NSLog().
That way you wouldn't have to use -stringWithFormat, and it would look cleaner.
