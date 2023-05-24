# Rust CSV Files Reader

## What does the app do?
The app takes the *.csv* file path as a program argument and tries to read it and print all its lines within the standard output file.

## Programming Languages:
- Rust

## Frameworks & Libraries:
- csv - https://docs.rs/csv/latest/csv/

## Implementation:
First step is to check if the user passes the path to the *.csv* file as a program argument, otherwise throw an error with a message that tells him how to run it correctly:
```rust
let program_arguments = std::env::args().collect::<Vec<String>>();
if 2 != program_arguments.len() {
    eprintln!("Usage: {} <csv-filename>", &program_arguments[0]);
    return;
}
```
After that, if the file exists and can be opened its lines will be printed, else an error will be thrown and the program will finish its execution:
```rust
let input_file_name = &program_arguments[1];
match read_csv_file(&input_file_name) {
    Ok(file_lines) => {
        println!("File content:");
        for line in file_lines.iter() {
            println!("{:?}", line);
        }
    }
    Err(error) => {
        eprintln!("Error occurred while reading \"{}\". Program exited with error: {}", input_file_name, error);
    }
}
```
