<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Upload PDF File</title>
    <style>
        body 
        {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f8f9fa;
        }
        .upload-container 
        {
            text-align: center;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 400px;
        }
        .drop-zone 
        {
            border: 2px dashed #ccc;
            padding: 20px;
            margin-top: 10px;
            cursor: pointer;
            border-radius: 5px;
            min-height: 100px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .drop-zone.highlight 
        {
            border-color: #007bff;
        }
        .file-list 
        {
            list-style: none;
            padding: 0;
            margin: 10px 0 0;
            width: 100%;
            max-height: 150px;
            overflow-y: auto;
        }
        .file-list li 
        {
            padding: 5px;
            border-bottom: 1px solid #eee;
            text-align: left;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .view-btn 
        {
            background-color: #28a745;
            color: white;
            padding: 3px 8px;
            border: none;
            cursor: pointer;
            border-radius: 3px;
            font-size: 12px;
        }
        .button 
        {
            padding: 10px 15px;
            margin: 10px;
            border: none;
            color: white;
            cursor: pointer;
            border-radius: 5px;
        }
        .save-btn { background-color: #dc3545; }
        .cancel-btn { background-color: #6c757d; }
        .choose-file-btn 
        {
            background-color: #007bff;
            padding: 10px 15px;
            border: none;
            color: white;
            cursor: pointer;
            border-radius: 5px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="upload-container">
        <h2>Upload PDF File</h2>
        <input type="file" id="fileInput" accept="application/pdf" multiple hidden>
        <button class="choose-file-btn" onclick="fileInput.click()">Choose PDF File</button>
        <div class="drop-zone" id="dropZone">
            <p id="dropText">You can drag and drop files here to add them.</p>
            <ul id="fileList" class="file-list"></ul>
        </div>

        <button class="button save-btn" onclick="saveFile()">Save Changes</button>
        <button class="button cancel-btn" onclick="cancelUpload()">Cancel</button>
    </div>
    
    <script>
        const dropZone = document.getElementById("dropZone");
        const fileInput = document.getElementById("fileInput");
        const fileList = document.getElementById("fileList");
        const dropText = document.getElementById("dropText");

        let uploadedFiles = [];

        dropZone.addEventListener("click", () => fileInput.click());
        dropZone.addEventListener("dragover", (e) => 
        {
            e.preventDefault();
            dropZone.classList.add("highlight");
        });
        dropZone.addEventListener("dragleave", () => dropZone.classList.remove("highlight"));
        dropZone.addEventListener("drop", (e) => 
        {
            e.preventDefault();
            dropZone.classList.remove("highlight");
            handleFiles(e.dataTransfer.files);
        });

        fileInput.addEventListener("change", () => handleFiles(fileInput.files));

        function handleFiles(files) 
        {
            Array.from(files).forEach((file) => {
                if (file.type === "application/pdf") 
                {
                    const fileURL = URL.createObjectURL(file);
                    uploadedFiles.push(
                    { 
                        name: file.name, 
                        size: (file.size / 1024).toFixed(2) + " KB", 
                        date: new Date().toLocaleString(),
                        url: fileURL 
                    });
                }
            });

            updateFileList();
        }

        function updateFileList() {
            fileList.innerHTML = "";
            uploadedFiles.forEach((file, index) => {
                const listItem = document.createElement("li");
                listItem.innerHTML = `${index + 1}. ${file.name} <button class="view-btn" onclick="viewFile('${file.url}')">View</button>`;
                fileList.appendChild(listItem);
            });

            dropText.style.display = uploadedFiles.length ? "none" : "block";
        }

        function viewFile(url) {
            window.open(url, "_blank"); 
        }

        function saveFile() {
            if (uploadedFiles.length > 0) 
            {
                sessionStorage.setItem("uploadedFiles", JSON.stringify(uploadedFiles));
                window.location.href = "file_details.html";
            } else 
            {
                alert("No file selected.");
            }
        }

        function cancelUpload() 
        {
            uploadedFiles = [];
            fileList.innerHTML = "";
            dropText.style.display = "block";
        }
    </script>
</body>
</html>
