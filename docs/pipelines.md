function exportSheetToGoogleDocWithDropdowns() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const doc = DocumentApp.create("Sheet Export with Dropdowns");
  const body = doc.getBody();

  const range = sheet.getDataRange();
  const values = range.getValues();
  const validations = range.getDataValidations();

  // Add a heading
  body.appendParagraph("📋 Sheet Export with Dropdown Details").setHeading(DocumentApp.ParagraphHeading.HEADING1);
  body.appendParagraph(`📅 Exported on: ${new Date().toLocaleString()}`);
  body.appendHorizontalRule();

  for (let i = 0; i < values.length; i++) {
    let rowText = '';
    for (let j = 0; j < values[i].length; j++) {
      const cellValue = values[i][j];
      const validation = validations[i][j];
      let cellText = `"${cellValue}"`;

      if (validation && validation.getCriteriaType() === SpreadsheetApp.DataValidationCriteria.VALUE_IN_LIST) {
        const options = validation.getCriteriaValues()[0];
        cellText += ` (Dropdown Options: ${options.join(', ')})`;
      }

      rowText += `Column ${String.fromCharCode(65 + j)}: ${cellText}  |  `;
    }
    body.appendParagraph(rowText.trim());
  }

  Logger.log("✅ Document created at: " + doc.getUrl());
  SpreadsheetApp.getUi().alert("✅ Done! Open your new Doc here:\n" + doc.getUrl());
}
