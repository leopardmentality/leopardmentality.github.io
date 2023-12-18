---
layout: post
title: Learning Log
date: 2023-12-17 8:00 -0600
categories: [Language Learning, Mandarin, Duolingo, Rosetta Stone]
tags: [Learning tools, Mandarin]
permalink: /posts/learning-log/
---
# Mandarin Learning Log

<div id="learning-log-container" style="text-align: center;">
  <table>
    <thead>
      <tr>
        <th>Day</th>
        <th>Words Learned</th>
        <th>Word Meanings</th>
        <th>Notes</th>
        <th>Edit</th>
        <th>Delete</th>
      </tr>
    </thead>
    <tbody id="learning-log-table-body">
      <!-- Previous entries will be dynamically loaded here using JavaScript -->
    </tbody>
  </table>

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
</div>

<script>
  document.addEventListener('DOMContentLoaded', function () {
    let learningLogData = [];

    function generateTable(data) {
      const tableBody = document.getElementById('learning-log-table-body');

      // Clear existing rows
      tableBody.innerHTML = '';

      for (let i = 0; i < data.length; i++) {
        const row = tableBody.insertRow();
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
    }

    function addEntry() {
      const day = document.getElementById('day').value;
      const wordsLearned = document.getElementById('words-learned').value;
      const wordMeanings = document.getElementById('word-meanings').value;
      const notes = document.getElementById('notes').value;

      if (day && wordsLearned && wordMeanings && notes) {
        const newEntry = { Day: day, 'Words Learned': wordsLearned, 'Word Meanings': wordMeanings, Notes: notes };
        learningLogData.push(newEntry);
        generateTable(learningLogData);
      } else {
        alert('Please fill in all fields.');
      }
    }

    function editEntry(index) {
      const entry = learningLogData[index];
      document.getElementById('day').value = entry.Day;
      document.getElementById('words-learned').value = entry['Words Learned'];
      document.getElementById('word-meanings').value = entry['Word Meanings'];
      document.getElementById('notes').value = entry.Notes;

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
