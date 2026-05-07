<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Notes Taking App</title>

    <style>

        *{
            margin:0;
            padding:0;
            box-sizing:border-box;
            font-family:Arial;
        }

        body{
            background:grey;
            min-height:100vh;
            padding:30px;
        }

        h1{
            text-align:center;
            color:black;
            margin-bottom:30px;
        }

        .container{
            width:90%;
            max-width:700px;
            margin:auto;
        }

        .note-box{
            background:white;
            padding:20px;
            border-radius:10px;
            margin-bottom:20px;
            box-shadow:0 0 10px rgba(0,0,0,0.2);
        }

        input{
            width:100%;
            padding:12px;
            margin-bottom:10px;
            font-size:16px;
        }

        textarea{
            width:100%;
            height:120px;
            padding:12px;
            font-size:16px;
            resize:none;
        }

        button{
            padding:10px 20px;
            margin-top:10px;
            border:none;
            background:blue;
            color:white;
            font-size:16px;
            border-radius:5px;
            cursor:pointer;
        }

        button:hover{
            background:#434190;
        }

        .notes{
            margin-top:20px;
        }

        .note{
            background:white;
            padding:15px;
            border-radius:10px;
            margin-bottom:15px;
            box-shadow:0 0 10px rgba(0,0,0,0.2);
        }

        .note h3{
            margin-bottom:10px;
            color:#333;
        }

        .note p{
            margin-bottom:10px;
            color:#555;
        }

        .delete-btn{
            background:red;
        }

        .delete-btn:hover{
            background:darkred;
        }

    </style>

</head>

<body>

    <h1>Notes Taking App</h1>

    <div class="container">

        <div class="note-box">

            <input type="text" id="title" placeholder="Enter Note Title">

            <textarea id="content" placeholder="Write your note here..."></textarea>

            <button onclick="addNote()">Add Note</button>

        </div>

        <div class="notes" id="notesContainer">

        </div>

    </div>

    <script>

        let notes = JSON.parse(localStorage.getItem("notes")) || [];

        displayNotes();

        function addNote()
        {

            let title = document.getElementById("title").value;

            let content = document.getElementById("content").value;

            if(title == "" || content == "")
            {
                alert("Please fill all fields");
                return;
            }

            let note = {
                title : title,
                content : content
            };

            notes.push(note);

            localStorage.setItem("notes", JSON.stringify(notes));

            document.getElementById("title").value = "";

            document.getElementById("content").value = "";

            displayNotes();

        }

        function displayNotes()
        {

            let container = document.getElementById("notesContainer");

            container.innerHTML = "";

            for(let i=0; i<notes.length; i++)
            {

                container.innerHTML += `

                <div class="note">

                    <h3>${notes[i].title}</h3>

                    <p>${notes[i].content}</p>

                    <button class="delete-btn"
                    onclick="deleteNote(${i})">

                    Delete

                    </button>

                </div>

                `;

            }

        }

        function deleteNote(index)
        {

            notes.splice(index,1);

            localStorage.setItem("notes", JSON.stringify(notes));

            displayNotes();

        }

    </script>

</body>

</html>
