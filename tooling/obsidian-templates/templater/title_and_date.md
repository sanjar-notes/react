<%*
retVal = tp.file.title;
if (retVal.endsWith(".md")) retVal = retVal.slice(0, -3);

completeTitle = retVal.replaceAll("_", " ");
potentialNumber = completeTitle.split(" ").at(0);
hasNumber = !Number.isNaN(parseFloat(potentialNumber));
titleWithoutNumber = completeTitle.slice(potentialNumber.length + 1);

newTitle = hasNumber
  ? `${potentialNumber}. ${titleWithoutNumber}`
  : completeTitle;
%># <% newTitle %>
<% tp.date.now("[Created] ddd ll [at] LT") %>

<% tp.file.cursor() %>