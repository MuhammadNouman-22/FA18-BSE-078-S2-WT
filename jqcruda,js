$(function() {
  loadRecipies();
  $("#albums").on("click", ".btn-danger", handleDelete);
  $("#albums").on("click", ".btn-warning", handleUpdate);
  $("#addBtn").click(addRecipe);
  $("#updateSave").click(function() {
    var id = $("#updateId").val();
    var title = $("#updateTitle").val();
    $.ajax({
      url: "https://jsonplaceholder.typicode.com/albums/" + id,
      data: { title },
      method: "PUT",
      success: function(response) {
        console.log(response);
        loadRecipies();
        $("#updateModal").modal("hide");
      }
    });
  });
});
function handleUpdate() {
  var btn = $(this);
  var parentDiv = btn.closest(".recipe");
  let id = parentDiv.attr("data-id");
  $.get("https://jsonplaceholder.typicode.com/albums/" + id, function(
    response
  ) {
    $("#updateId").val(response.id);
    $("#updateTitle").val(response.title);
    $("#updateModal").modal("show");
  });
}
function addRecipe() {
  var title = $("#title").val();

  $.ajax({
    url: "https://jsonplaceholder.typicode.com/albums",
    method: "POST",
    data: { title },
    success: function(response) {
      console.log(response);
      $("#title").val("");

      loadRecipies();
      $("#addModal").modal("hide");
    }
  });
}
function handleDelete() {
  var btn = $(this);
  var parentDiv = btn.closest(".recipe");
  let id = parentDiv.attr("data-id");
  console.log(id);
  $.ajax({
    url: "https://jsonplaceholder.typicode.com/albums/" + id,
    method: "DELETE",
    success: function() {
      loadRecipies();
    }
  });
}
function loadRecipies() {
  $.ajax({
    url: "https://jsonplaceholder.typicode.com/albums",
    method: "GET",
    error: function(response) {
      var albums = $("#albums");
      albums.html("An Error has occured");
    },
    success: function(response) {
      console.log(response);
      var albums = $("#albums");
      albums.empty();
      for (var i = 0; i < response.length; i++) {
        var rec = response[i];
        albums.append(
          `<div class="recipe" data-id="${rec.id}"><h3>${rec.title}</h3><p><button class="btn btn-danger btn-sm float-right">delete</button><button class="btn btn-warning btn-sm float-right">Edit</button></p><br></div>`
        );
        // albums.append("<div><h3>" + rec.title + "</h3></div>");
      }
    }
  });
}
