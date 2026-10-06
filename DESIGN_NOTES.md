# Campus Resource Assistant - Design Notes

## 1. Problem Statement

Student Services wants us to create a Campus Resource Assistant that makes it easier for students to find information about services offered by the college. Students may not know where to find information such as library hours, tutoring, academic advising, or financial aid. The assistant will allow students to ask questions in normal English and receive useful answers based on information that has been verified by the college.

## 2. Why Gemini Cannot Answer Campus-Specific Questions by Itself

Gemini is trained on large amounts of general information, but it does not automatically have access to current information specific to the college. Information such as office locations, phone numbers, staff, and hours can also change. If Gemini tries to answer these questions using only what it learned during training, it could give outdated or incorrect information. Giving the agent a tool that reads a verified local data file allows it to retrieve the information instead of guessing.

## 3. Why Store Campus Data in JSON?

There are several reasons to store the campus information in a JSON file instead of directly inside the Python function.

1. JSON separates the data from the program logic. Campus information can be updated without changing the Python code.
2. The information can be reviewed and verified by someone who does not understand Python.
3. JSON makes it easier to expand the project later. The JSON file could eventually be replaced by a database, API, or another data source without redesigning the entire agent.

## 4. Three Limitations and Future Improvements

### Data can become outdated
Office hours, staff, and locations can change. A future version could retrieve information from an official college API or another live college data source.

### No long-term memory
The current agent does not remember previous conversations. A future version could store approved conversation information in a database or persistent session system.

### The model may fail to call the tool
Because an LLM is probabilistic, Gemini may occasionally answer without using the campus resource tool. This could be improved with clearer agent instructions, a stronger tool description, additional testing, and automated tests.

## 5. Accuracy and Verification

If the information in the JSON file is inaccurate, the agent could give students incorrect information even though the software is working correctly. For example, a student could be sent to the wrong building or given an incorrect phone number. Campus information should be verified against official college sources and periodically reviewed by the college staff responsible for each service. The verified_by and last_verified fields help track who checked the information and when it was checked.

## Campus Resource Research

The campus resource information used by the agent will be researched using official college sources. Information that cannot be verified will be marked for review rather than guessed.