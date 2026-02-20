---
title: "books"
permalink: /books/
layout: single
author_profile: true
classes: wide
---

{% assign rating_labels = "Avoid,OK,Good,Great,Amazing" | split: "," %}
{% assign star_strings = "★☆☆☆☆,★★☆☆☆,★★★☆☆,★★★★☆,★★★★★" | split: "," %}
{% assign sorted_books = site.books | sort: "date_finished" | reverse %}
{% assign all_genres = "" | split: "" %}
{% for book in sorted_books %}
  {% if book.genres %}
    {% assign genre_arr = book.genres | join: "|" | split: "|" %}
    {% assign all_genres = all_genres | concat: genre_arr %}
  {% endif %}
{% endfor %}
{% assign all_genres = all_genres | uniq | sort %}

<style>
.books-table {
  width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
}
.books-table thead,
.books-table tfoot {
  display: table;
  width: 100%;
  table-layout: fixed;
}
.books-table tbody {
  display: block;
  max-height: 70vh;
  overflow-y: auto;
}
.books-table tbody tr {
  display: table;
  width: 100%;
  table-layout: fixed;
}
.books-table th:nth-child(1), .books-table td:nth-child(1) { width: 25%; }
.books-table th:nth-child(2), .books-table td:nth-child(2) { width: 19%; }
.books-table th:nth-child(3), .books-table td:nth-child(3) { width: 17%; }
.books-table th:nth-child(4), .books-table td:nth-child(4) { width: 12%; white-space: nowrap; }
.books-table th:nth-child(5), .books-table td:nth-child(5) { width: 13%; }
.books-table th:nth-child(6), .books-table td:nth-child(6) { width: 14%; }
.books-table tfoot {
  background-color: #cecfd1;
}
.books-table tfoot td {
  font-size: 0.85em;
  font-style: italic;
}

/* Filter toggle button */
.books-filter-toggle {
  padding: 4px 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.85em;
  background: none;
  cursor: pointer;
  color: #555;
  margin-bottom: 6px;
}
.books-filter-toggle:hover { background: #f0f0f0; }

/* Filter bar */
.books-filter {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 8px;
  align-items: center;
}
.books-filter input,
.books-filter select {
  padding: 5px 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.85em;
  min-width: 130px;
}
.books-filter-clear {
  padding: 5px 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.85em;
  background: none;
  cursor: pointer;
  color: #555;
}
.books-filter-clear:hover { background: #f0f0f0; }

@media (max-width: 600px) {
  .books-table th:nth-child(6),
  .books-table td:nth-child(6) { display: none; }

  .books-table th:nth-child(1), .books-table td:nth-child(1) { width: 26%; }
  .books-table th:nth-child(2), .books-table td:nth-child(2) { width: 20%; }
  .books-table th:nth-child(3), .books-table td:nth-child(3) { width: 14%; }
  .books-table th:nth-child(4), .books-table td:nth-child(4) { width: 18%; }
  .books-table th:nth-child(5), .books-table td:nth-child(5) { width: 22%; }
}
</style>

<button id="filter-toggle" class="books-filter-toggle">Filters ▼</button>
<div class="books-filter" style="display:none">
  <input  type="search" id="filter-author" placeholder="Author…" autocomplete="off">
  <input  type="search" id="filter-series" placeholder="Series…" autocomplete="off">
  <select id="filter-rating">
    <option value="">Any rating</option>
    <option value="5">★★★★★</option>
    <option value="4">★★★★☆</option>
    <option value="3">★★★☆☆</option>
    <option value="2">★★☆☆☆</option>
    <option value="1">★☆☆☆☆</option>
  </select>
  <select id="filter-genre">
    <option value="">All genres</option>
    {% for genre in all_genres %}
    <option value="{{ genre }}">{{ genre | replace: "-", " " | capitalize }}</option>
    {% endfor %}
  </select>
  <button id="filter-clear" class="books-filter-clear">Clear</button>
</div>

<table class="books-table">
  <thead>
    <tr>
      <th>Title</th>
      <th>Author</th>
      <th>Series</th>
      <th title="★☆☆☆☆ Avoid
★★☆☆☆ OK
★★★☆☆ Good
★★★★☆ Great
★★★★★ Amazing" style="cursor:help">Rating</th>
      <th>Finished</th>
      <th>Genre(s)</th>
    </tr>
  </thead>
  <tbody>
    {% for book in sorted_books %}
    {% assign label_index = book.rating | minus: 1 %}
    {% assign label = rating_labels[label_index] %}
    {% assign stars = star_strings[label_index] %}
    <tr data-author="{{ book.author | downcase }}"
        data-series="{{ book.series | downcase }}"
        data-rating="{{ book.rating }}"
        data-genres="{{ book.genres | join: '|' | downcase }}">
      <td>{% assign has_notes = book.content | strip | size %}{% if has_notes > 0 %}<a href="{{ book.url }}">{{ book.title }}</a>{% else %}{{ book.title }}{% endif %}</td>
      <td>{{ book.author }}</td>
      <td>{% if book.series %}{{ book.series }}{% if book.series_number %} #{{ book.series_number }}{% endif %}{% endif %}</td>
      <td><span title="{{ label }}">{{ stars }}</span></td>
      <td>{{ book.date_finished | date: "%b %-d, %Y" }}</td>
      <td>{{ book.genres | join: ", " }}</td>
    </tr>
    {% endfor %}
    <tr id="books-no-results" style="display:none">
      <td colspan="6" style="text-align:center;color:#888;padding:1em;">No books match the current filters.</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="6" id="books-count" style="text-align:right"></td>
    </tr>
  </tfoot>
</table>

<script>
(function () {
  const TOTAL = document.querySelectorAll('.books-table tbody tr[data-rating]').length;

  function applyFilters() {
    const author = document.getElementById('filter-author').value.toLowerCase().trim();
    const genre  = document.getElementById('filter-genre').value;   // already lowercase
    const series = document.getElementById('filter-series').value.toLowerCase().trim();
    const rating = parseInt(document.getElementById('filter-rating').value) || 0;

    let visible = 0;
    document.querySelectorAll('.books-table tbody tr[data-rating]').forEach(row => {
      const match =
        (!author || row.dataset.author.includes(author)) &&
        (!genre  || row.dataset.genres.split('|').includes(genre)) &&
        (!series || row.dataset.series.includes(series)) &&
        (!rating || parseInt(row.dataset.rating) === rating);
      row.style.display = match ? '' : 'none';
      if (match) visible++;
    });

    document.getElementById('books-count').textContent =
      visible === TOTAL ? `${TOTAL} books` : `${visible} of ${TOTAL} books`;
    document.getElementById('books-no-results').style.display = visible === 0 ? '' : 'none';
  }

  ['filter-author', 'filter-genre', 'filter-series', 'filter-rating'].forEach(id => {
    document.getElementById(id).addEventListener('input', applyFilters);
  });

  document.getElementById('filter-clear').addEventListener('click', () => {
    document.getElementById('filter-author').value = '';
    document.getElementById('filter-genre').value  = '';
    document.getElementById('filter-series').value = '';
    document.getElementById('filter-rating').value = '';
    applyFilters();
  });

  // Toggle filter bar
  document.getElementById('filter-toggle').addEventListener('click', () => {
    const bar = document.querySelector('.books-filter');
    const btn = document.getElementById('filter-toggle');
    const open = bar.style.display === 'none';
    bar.style.display = open ? '' : 'none';
    btn.textContent = open ? 'Filters ▲' : 'Filters ▼';
  });

  // Show initial count
  applyFilters();
})();
</script>
