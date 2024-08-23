# Predict-war-from-statcast-data
Project to predict the WAR (Wins above Replacement) of a player from the full season publicly available Statcast data (2015-2023)

Statcast_download and Statcast_download_clean contain the data that was downloaded from Baseball Savant. The Statcast_download file also contains the excel cleaning functions that were undertook in order to clean the names. This data was then imported into MySQL using the Table Data Import Wizard.

In Excel, to clean the names of the players, I wrote a RemoveAccents function in VBA as 
Function RemoveAccents(ByVal text As String) As String
    Dim AccChars As String
    Dim RegChars As String
    Dim i As Integer

    AccChars = "áàäâãåÁÀÄÂÃÅéèëêÉÈËÊíìïîÍÌÏÎóòöôõÓÒÖÔÕúùüûÚÙÜÛñÑçÇ"
    RegChars = "aaaaaaAAAAAAeeeeEEEEiiiiIIIIoooooOOOOOuuuuUUUUnNcC"

    For i = 1 To Len(AccChars)
        text = Replace(text, Mid(AccChars, i, 1), Mid(RegChars, i, 1))
    Next i

    RemoveAccents = text
End Function

After that, I removed the # and * that were at the end of the names after downloading from baseball reference using a substitute function. I did the same to remove periods within the names. Finally, I made the names lowercase and without any spaces so that they could be used as an identifier along with plate appearances and year. This identifier was chosen because it was universal between the baseball reference and baseball savant data. 
