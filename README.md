
## CreateTask
+ req
+ res
```javascript
async function createTask(req, res) {

    try {
        // get all data from body
        const { title, description, status } = req.body;
        const newTask = await Task.create({

            title,

            description,

            status,

        });

        if (newTask) {

            return res.status(201).json({ message: "succussfylly created new task", task: newTask });

        }

    } catch (error) {

        return res.status(500).json({ message: "Internal server error", error: error.message });

    }

}



```

### usage this code
To create a new task and save it to the database using the data sent in the request body.

 
## GetAllTasks

+ req
+ res

```javascript
async function tasks(req, res) {

    try {

        const getllAllTask = await Task.find();

        if (getllAllTask) {

            return res.status(201).json({ message: "task fetched succussFully", alltask: getllAllTask });

        }

    } catch (error) {

        return res.status(500).json({ message: "data fetching server error", error: error.message });

    }

}


```

### usage this function 
get all tasks from task database

##  DeleteTask

+ req
+ res
 ```javaScript
 async function deleteTask(req, res) {

    try {

        const { id } = req.body;

  

        if (!id) {

            return res.status(400).json({ message: "not provided task id" });

        }

        const getTask = await Task.findOne({ _id: id });

        if (!getTask) {

            return res.status(404).json({ message: "this task not founded in database" });

        }

  

        const deleteTask = await Task.findByIdAndDelete(id);

        if (deleteTask) {

            return res.status(201).json({ message: "succussFully deleted", deleteTask });

        }

    } catch (error) {

        return res.status(500).json({ message: "Internal server error", error: error.message });

    }

}
 
```
## updateTask
```javascript
async function updateTask(req, res) {

    try {

        console.log(req.body);

        const { id, status } = req.body;

  

        if (!id) {

            return res.status(400).json("id not provided");

        }

  

        const getTask = await Task.findOne({ _id: id });

  

        if (!getTask) {

            return res.status(404).json({ message: "this task not founded in database" });

        }

  

        if (!status) {

            return res.status(400).json({ message: "All fields are required" });

        }

  

        const updateTask = await Task.findByIdAndUpdate({ _id: id }, { $set: { status: status } }, { new: true });

  

        if (updateTask) {

            return res.status(201).json({ message: "task succussFully Updated", updateTask });

        }

    } catch (error) {

        return res.status(500).json({ message: "Internal server error", error: error.message });

    }

}



```

### usage this code

To update the **status** of an existing task using the task's ID received in the request body.


   
