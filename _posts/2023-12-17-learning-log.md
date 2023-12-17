---
layout: post
title: "Mandarin Learning Log"
categories: [Language Learning, Mandarin, Duolingo, Rosetta Stone]
---

# Mandarin Learning Log

<div id="learning-log-container" style="text-align: center;"></div>

<form id="learning-log-form">
  <label for="day">Day:</label>
  <input type="number" id="day" required>

  <label for="words-learned">Words Learned:</label>
  <input type="text" id="words-learned" required>

  <label for="word-meanings">Word Meanings:</label>
  <input type="text" id="word-meanings" required>

  <label for="notes">Notes:</label>
  <textarea id="notes" required></textarea>

  <button type="button" onclick="addEntry()">Add Entry</button>
</form>

<script>
  document.addEventListener('DOMContentLoaded', function () {
    let learningLogData = [];

    function generateTable(data) {
      const tableContainer = document.getElementById('learning-log-container');
      const table = document.createElement('table');
      const headerRow = table.insertRow(0);

      for (const key in data[0]) {
        const header = document.createElement('th');
        header.textContent = key.charAt(0).toUpperCase() + key.slice(1);
        headerRow.appendChild(header);
      }

      for (let i = 0; i < data.length; i++) {
        const row = table.insertRow();
        for (const key in data[i]) {
          const cell = row.insertCell();
          cell.textContent = data[i][key];
        }

        const editCell = row.insertCell();
        const editButton = document.createElement('button');
        editButton.textContent = 'Edit';
        editButton.onclick = function () { editEntry(i); };
        editCell.appendChild(editButton);

        const deleteCell = row.insertCell();
        const deleteButton = document.createElement('button');
        deleteButton.textContent = 'Delete';
        deleteButton.onclick = function () { deleteEntry(i); };
        deleteCell.appendChild(deleteButton);
      }

      tableContainer.innerHTML = '';
      tableContainer.appendChild(table);
    }

    function addEntry() {
      const day = document.getElementById('day').value;
      const wordsLearned = document.getElementById('words-learned').value;
      const wordMeanings = document.getElementById('word-meanings').value;
      const notes = document.getElementById('notes').value;

      if (day && wordsLearned && wordMeanings && notes) {
        const newEntry = { day: day, 'words learned': wordsLearned, 'word meanings': wordMeanings, notes: notes };
        learningLogData.push(newEntry);
        generateTable(learningLogData);
      } else {
        alert('Please fill in all fields.');
      }
    }

    function editEntry(index) {
      const entry = learningLogData[index];
      document.getElementById('day').value = entry.day;
      document.getElementById('words-learned').value = entry['words learned'];
      document.getElementById('word-meanings').value = entry['word meanings'];
      document.getElementById('notes').value = entry.notes;

      learningLogData.splice(index, 1);
      generateTable(learningLogData);
    }

    function deleteEntry(index) {
      learningLogData.splice(index, 1);
      generateTable(learningLogData);
    }

    generateTable(learningLogData);
  });
</script>
