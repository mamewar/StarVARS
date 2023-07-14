# StarVARS

Tuesday, July 4, 2023 11:42 AM





**ImageSubtractionHelper.cs**



|Methods|Parameter|Description|Return Type|
| - | - | - | - |
|ShowSubtractedImage(image1 , image2)|String, String|Shows subtracted image in new tab.|String. Returns the path to new tab.|
|saveSubtractedImage(image1,image2)|String, String|Saves subtracted image in downloads folder.|Int. Returns 1 if success else 0.|

**Plotter.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|Plot(xAxis,yAxis)  |String, String|shows plots between x-axis and y-axis in new tab.|String. Returns the path to new tab.|
|parsElementValues(element,value)|String, List<double>|This method has dependency on plot(x,y). Parses all xml files and creates list of coordinates of where element tag is present.|void. populates the value parameter  with coordinates.|

**CreateTreeView.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|CreateTreeView(files)  |HashSet<string>|Creates a tree structure|HashSet<TreeItem>. Return Hashset which contains the treeview. Just add reference of this return type in the builtin treeview of mudblazor. |
|CreateTreeView(files, checkboxfilepath)|HashSet<string>,Dictionary <string, string> |Creates a tree structure and also updates the dictionary which stores file full path, just file name|HashSet<TreeItem>. Return Hashset which contains the treeview. Just add reference of this return type in the builtin treeview of mudblazor. |

New Section 1 Page 1

**WebPConvertor.cs**



|Method|Parameter|Description|Return type|
| - | - | - | - |
|ConvertToWebP(inputPath, outputPath, imageQualityPercentage)|String, String, Integer|Creates a webp instance with image quality and calls ConvertImageToWebP()|Void|
|ConvertImageToWebP(inputPath, outputPath, outputImageFormat)|String , String, ISupportedImageFor mat|Reads image from inputpath, converts image to webp and saves it in outputpath|Void|

**XmlDiffrenceHelper.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|findDifference(xmlText1,xmlText2)|String, String|Finds difference among 2 files using DiffPlex Nuget package.|string. Differenced xml string.|
|tokenizeXml(xmlText)|String|Has dependency on findDifference(). Reads xml text from xml file and breaks it into tags and values|String. Returns tokenized xml.|
|IndentXmlTags(xmlText, indentationLevel)|String, Integer|Has dependency on findDifference(). Applies required indentation to the line and return the indented line.|String. Returns indented line|
|EncodeXmlTags (xmlLineText)|String(xml text line)|Has dependency on tokenizeXml(). Converts tags so that they render on html page.|String. Returns html friendly tag.|

**ZipConvertor.cs**



|Method|Parameter|Description|Return type|
| - | - | - | - |
|CreateZip(files, Savepath)|HashSet<string>, string |Iterate over all files convert them to zip and saves in the path specified.|void|

**StarvarsHomePageHelper.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|LoadConfig()||Reads the config file appsettings.json and calls LoadFilter()|Void|
|LoadFilter(config)|JObject|Has dependency on LoadConfig(). Selects the selector which user has choosen and adds a filter in \_filter|Void|
|FolderExists()||Checks if folder exists|bool|
|AddFolderToList()||Add folder to the list of folders.|Void|
|UpdateList()||Calls FilterFilesByRegex()|Void|
|FilterFilesByRegex()||Updates files based on filters applied|Void|
|LoadFileNames()||Iterate over all folders and add the files inside them to fileList.|Void|



|Class||
| - | :- |
|FileType|Stores extension and files count.|

New Section 1 Page 2

**ImageViewHelper.cs**



|Method|Parameter|Description|Return type|
| - | - | - | - |
|ImageViewHelper()|HashSet<string>, string |Iterate over all files convert them to zip and saves in the path specified.|Void|

**XmlToCsvHelper.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|CreateCSV(destination Folder, files)|String, List<string>|Collects all tags inside xml and creates a csv file and saves it to destination Folder |Void|
|AddRowForXML(FileCounter, csv, dictionary)|Integer, CSVFile, dictionary|Creates a new row in CSV file.|Void|
|viewRelatedImages(file)|String|Extracts images present in a xml file.|List<string>. Returns list of images|
|getImageNameTags()||Has dependency on viewRelatedImages(). Creates a list of Image Tags to search for while Extracting Images.|List<string>. Return list of tags.|
|||||
|**Class Name**||||
|**CSVFile**||||
|Method|Parameter|Description|Return Type|
|AddData(row, column, value)|Int , String, String |Add value at row, column. |Void|
|SaveFile()||Saves the file at desired location (\_Filename)|Void|
|||||
|**XMLParser**||||
|Method|Parameter|Description|Return Type|
|ExtractData()||Iterate all xml files and creates a dictionary of xml tags vs xml value|Dictionary<string, string>|

**XmlViewHelper.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|UpdateCurrentList()||Updates the xml file list based on filters applied.|Void
|Dooperation(Object)|Object of type tuple|Has dependency on UpdateCurrentList(). Tuple has start and end index of xml files this function has to iterate over. Save filtered files in a list called \_filteredFilesPerThread.|Void
|UpdateList()||Updates the xml file list based on filters applied.|Void
|SaveToCSV()||Selects all xml files which are checked and calls CreateCsv() of xmlToCsvHelper class|Void
|DownloadZip()| |Selects all  xml files which are checked and calls CreateZip of ZipConvertor class.|Void
|OpenRelatedImages(filename)| String |Returns list of image names associated with file. Calls viewRelatedImages() of xmlToCsvHelper class.|List<string>

**Code behind files of Pages ImageView.razor.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|CheckboxClicked(image name, checkedvalue)|String, object|Adds or removes the image based on its checkedvalue. Also shows the last image selected and its details ( date modified, date created, size)|Void|
|ShowSubtractedImage()||Selected the last 2 selected images and calls ImageSubtractionHelper.showSubtractedImage(). Opens a newtab to view.|Void|
|SaveSubtractedImages()||Selects the last 2 selected images and calls ImageSubtractionHelper.saveSubtractedImage().|Void|
|DownloadImages()||Downloads all selected images in zip file. Calls ZipConvertor class.|Void|

**PlotterView.razor.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|DrawLineGraph()||Calls the plotlyInterop javascript file in wwwroot/js and generates the plots.|Async Task|
|DownloadCoordinates()||Saves the coordinates in csv file.|Void|

**StarVarsHomePage.razor.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|AddFolder()||Adds folder to folder list if it exists and calls treeview class to create a treeview for folder files.|Void|
|CreateTreeView()||Update the files based on filters and creates the treeview based on filtered files. Calls TreeViewHelper class.|Void|
|findFiles()||Redirect to respective tab based on the extension.|Void|
|RemoveFolder()||Remove a folder from folder list and update the treeview.|Void|

**XmlView.razor.cs**



|Method|Parameter|Description|Return Type|
| - | - | - | - |
|UpdateFineFilterTable()||Updates the files based on the filter you applied and update treeview.|Void
|DeleteFilter( element, value, comparator)||Deletes the filter with element name as element, value as value and comparator as comparator. Update treeview. |Void
|ChangeDisableButtonState()||Enable or disable the button and update treeview accordingly.|Void
|currentXML(xmlfilepath)|String|Reads the xml file and save in xmlContent and shows in the view after beautifying the xml.|Void
|XmlPrettify(xmlText)|<p>String</p><p></p>|Beautify xml text.|String
|ColorizeXmlTags(xmlTextLine) | String | Colorize xml tags and return the colored line. | String
|OpenXmlInNewTab() | | Opens XML file in new tab. | Void 
|MasterCheckBoxClicked(checkvalue)| Object |If master checkbox is checked then check all checkboxes else uncheck all checkboxes. | Void
|CheckBoxClicked(xmlFileName, checkvalue)| String,object |Adds the xmlFileName to selected xml list and if checkbox is checked, else remove xmlFileName from selected xml list.| Void
|openRelatedImages(xmlFileName)| String |Opens related Images of an xml file in new tab. |Void

**Class Diagram**

![Class Diagram](https://assets.digitalocean.com/articles/alligator/boo.svg "a title")
