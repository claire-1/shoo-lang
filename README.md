# shoo-lang

[![CircleCI](https://circleci.com/gh/sam-jay/shoo-lang/tree/master.svg?style=svg)](https://circleci.com/gh/sam-jay/shoo-lang/tree/master)
[![Coverage Status](https://coveralls.io/repos/github/sam-jay/shoo-lang/badge.svg?branch=master)](https://coveralls.io/github/sam-jay/shoo-lang?branch=master)

## Table of Contents

- [Overview](#overview)
- [Requirements](#requirements)
- [Usage](#usage)
- [Sample Program](#sample-program)
- [Running Tests](#running-tests)

## Overview
This project is our compiler for the Fall 2018 Progamming Languages and Translators class at Columbia University taught by Professor Stephen Edwards. We worked a group to design our own programming language and compiler for it. The [Shoo_Final_Report.pdf](https://github.com/claire-1/shoo-lang/blob/master/final_report/Shoo_Final_Report.pdf) details the development of our language, how to write a program in our language, and the division of labor. 

## Requirements

Install OCaml and OPAM.
OCaml version 4.04.0 or higher is required.

* Install dependencies:
```sh
$ opam install ounit
```

## Usage

Build the compiler binary using make.

```sh
$ make
```

## Sample Program

Shoo is a programming language with C-like syntax while supporting first class functions, structs, and type inference.

Here is a sample program written in Shoo:

```
struct Professor {
  string name;
}

struct Student {
  string name;
  func(Professor;void) greet;
}

function createProfessor(string name) Professor {
  return { name = name; };
}

function createStudentCreator(string defaultGreeting) func(string;Student) {
  return function(string name) Student {
    function helper(int i) string {
      string x = "st";
      if (i == 0 || i == 4) {
        x = "th";
      } elif (i == 2) {
        x = "nd";
      } elif (i == 3) {
        x = "rd";
      }
      return str_of_int(i) + x;
    }
    return {
      name = name;
      greet = function(Professor p) void {
        for (int i = 0; i < 5; i = i + 1) {
          println(name + " says " + defaultGreeting + " to " + p.name + " for the " + helper(i) + " time");
        }
        return;
      };
    };
  };
}

Professor stephen = createProfessor("Stephen");

createStudentCreator("hello")("Sam").greet(stephen);
```

## Running Tests

Take a look inside testall.sh for the variables which set the path to the LLVM interpreter as variable "lli". 
Set the path to the LLVM compiler as "llc". Set the path to the C compiler as "cc".

```sh
$ make
$ ./testall.sh
```
