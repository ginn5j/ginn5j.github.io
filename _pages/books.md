---
title: "books"
permalink: /books/
layout: single
author_profile: true
classes: wide
---

{% assign rating_labels = "Abandoned or Disliked,OK,Good,Great,Amazing" | split: "," %}
{% assign star_strings = "★☆☆☆☆,★★☆☆☆,★★★☆☆,★★★★☆,★★★★★" | split: "," %}
{% assign sorted_books = site.books | sort: "date_finished" | reverse %}

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

<table class="books-table">
  <thead>
    <tr>
      <th>Title</th>
      <th>Author</th>
      <th>Series</th>
      <th>Rating</th>
      <th>Finished</th>
      <th>Genre(s)</th>
    </tr>
  </thead>
  <tbody>
    {% for book in sorted_books %}
    {% assign label_index = book.rating | minus: 1 %}
    {% assign label = rating_labels[label_index] %}
    {% assign stars = star_strings[label_index] %}
    <tr>
      <td>{% assign has_notes = book.content | strip | size %}{% if has_notes > 0 %}<a href="{{ book.url }}">{{ book.title }}</a>{% else %}{{ book.title }}{% endif %}</td>
      <td>{{ book.author }}</td>
      <td>{% if book.series %}{{ book.series }}{% if book.series_number %} #{{ book.series_number }}{% endif %}{% endif %}</td>
      <td><span title="{{ label }}">{{ stars }}</span></td>
      <td>{{ book.date_finished | date: "%b %-d, %Y" }}</td>
      <td>{{ book.genres | join: ", " }}</td>
    </tr>
    {% endfor %}
  </tbody>
  <tfoot>
    <tr>
      <td colspan="6">★☆☆☆☆ Abandoned or Disliked &nbsp;·&nbsp; ★★☆☆☆ OK &nbsp;·&nbsp; ★★★☆☆ Good &nbsp;·&nbsp; ★★★★☆ Great &nbsp;·&nbsp; ★★★★★ Amazing</td>
    </tr>
  </tfoot>
</table>
