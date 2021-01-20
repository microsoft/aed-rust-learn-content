# Knowledge Check

What is the purpose of the `structopt` third-party crate, used in the `cli` module of the command
line program?

- Parse the command line arguments provided by the user and place them in a struct.
  - Correct
- Parse the contents of the journal file into a vector of `Tasks`
  - Inorrect. That is the role fo the `serde_json` crate.
- Handle different types of errors seamlessly and display friendly error messages to users.
  - Inorrect. That is the role fo the `anyhow` crate.



What is the purpose of the `serde_json` third-party crate, used in the `tasks` module of the command
line program?

- Parse the contents of the journal file into a vector of `Tasks`
  - Correct
- Parse the command line arguments provided by the user and place them in a struct.
  - Inorrect. That is the role fo the `structopt` crate.
- Handle different types of errors seamlessly and display friendly error messages to users.
  - Inorrect. That is the role fo the `anyhow` crate.


What is the purpose of the `anyhow` third-party crate, used in the `main` module of the command
line program?

- Parse the contents of the journal file into a vector of `Tasks`
  - Inorrect. That is the role fo the `serde_json` crate.
- Parse the command line arguments provided by the user and place them in a struct.
  - Inorrect. That is the role fo the `structopt` crate.
- Handle different types of errors seamlessly and display friendly error messages to users.
  - Correct
