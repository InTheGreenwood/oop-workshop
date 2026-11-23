classDiagram
    class Library {
        -mediaCollection: List~Media~
        -users: List~User~
        +AddMedia(media: Media) void
        +RemoveMedia(media: Media) void
        +GetCollectionByType() List~T~
        +AddUser(user: User) void
        +RemoveUser(user: User) void
        +GetUsers() List~User~
    }

    class User {
        <<abstract>>
        #name: String
        #age: int
        #ssn: String
        +UserInfo() String
    }

    class Borrower {
        -borrowedMedia: List~Media~
        +Borrow(media: Media) void
        +Rate(media: Media, score: int) void
        +Return(media: Media) void
    }

    class Employee {
        +AddMedia(library: Library, media: Media) void
        +RemoveMedia(library: Library, media: Media) void
    }

    class Admin {
        +CreateUser(library: Library, user: User) void
        +DeleteUser(library: Library, user: User) void
        +UpdateUser(user: User, name: String, age: int, ssn: String) void
        +ViewUsers(library: Library) List~User~
    }

    class IRatable {
        <<interface>>
        +Rate(score: int) void
    }

    class IDownloadable {
        <<interface>>
        +Download() String
    }

    class IWatchable {
        <<interface>>
        +Watch() String
    }

    class IExecutable {
        <<interface>>
        +Execute() String
    }

    class IViewable {
        <<interface>>
        +View() String
    }

    class IReadable {
        <<interface>>
        +Read() String
    }

    class IDisplayable {
        <<interface>>
        +Display() String
    }

    class IListenable {
        <<interface>>
        +Listen() String
    }

    class ICompletable {
        <<interface>>
        +Complete() void
    }

    class IPlayable {
        <<interface>>
        +Play() String
    }

    class Media {
        <<abstract>>
        #title: String
        #isLoaned: bool
        #rating: double
        #numOfRatings: int
        +Borrow() void
        +Return() void
        +Show() String
        +Download() String
        +Rate(score: int) void
    }

    class Movie {
        -director: String
        -genre: List~String~
        -year: int
        -language: String
        -duration: int
        +Watch() String
    }

    class App {
        -version: String
        -publisher: String
        -platform: List~String~
        -size: int
        +Execute() String
    }

    class Ebook {
        -author: String
        -language: String
        -numPages: int
        -published: int
        -isbn: String
        +View() String
        +Read() String
    }

    class Image {
        -resolution: String
        -format: String
        -size: int
        -date: DateTime
        +Display() String
    }

    class Podcast {
        -host: List~String~
        -guest: List~String~
        -year: int
        -episodeNum: int
        -language: String
        -isCompleted: bool
        +Listen() String
        +Complete() void
    }

    class VideoGame {
        -genre: String
        -publisher: String
        -year: int
        -platform: List~String~
        -isCompleted: bool
        +Play() String
        +Complete() void
    }

    class Song {
        -composer: String
        -genre: String
        -singer: String
        -fileType: String
        -duration: int
        -language: String
        +Play() String
    }

    %% Library Relationships
    Library "1" o-- "0..*" Media : contains
    Library "1" o-- "0..*" User : manages

    %% User Hierarchy & Associations
    User <|-- Borrower
    User <|-- Employee
    Employee <|-- Admin
    Borrower "0..1" --> "0..*" Media : borrows
    Employee ..> Library : manages media in
    Admin ..> Library : manages users in

    %% Media Hierarchy & Interfaces
    IRatable <|.. Media
    IDownloadable <|.. Media

    Media <|-- Movie
    Media <|-- App
    Media <|-- Ebook
    Media <|-- Image
    Media <|-- Podcast
    Media <|-- VideoGame
    Media <|-- Song

    IWatchable <|.. Movie
    IExecutable <|.. App
    IViewable <|.. Ebook
    IReadable <|.. Ebook
    IDisplayable <|.. Image
    IListenable <|.. Podcast
    ICompletable <|.. Podcast
    ICompletable <|.. VideoGame
    IPlayable <|.. VideoGame
    IPlayable <|.. Song
