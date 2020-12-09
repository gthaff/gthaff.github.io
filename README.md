# Search
My first search engine!

# OOA
## OOA 1
Finding Classes and Objects
  Stoplist, InvertedIndex, Document
Finding Attributes
  stoplist, containIn, docIndex, documents, query, debug, name, originalText, editedText, invertedIndex
Finding Services
  addDocument, singleWordQuery, multiWordQuery, debug, hasQuery
Finding Inheritance
  None
Finding Delegation
  InvertedIndex has-a document and stoplist
  
## OOA 2
Class Stoplist
Finding Attributes:
  stoplist-             contains all of the stop words
Finding Services:

Class InvertedIndex
Finding Attributes:
  stoplist-             list of all stop words
  docIndex-             hashmap of query and documents that had the query
  containIn-            hashset of documents that had the query
  documents-            list of all documents
Finding Services:
  addDocument-          adds a document to the list of documents
  singleWordQuery-      finds if a single worded query is in the list of documents
  multiWordQuery-       finds if a phrase is in the list of documents
  debug-                dumps all information from the invertedindex

Class Document
Finding Attributes:
  name-                 name of the document
  originalText-         list of the words from the file with punctuation and spaces
  editedText-           list of the words from the file without punctuation and spaces
Finding Services:
  hasQuery-             checks if the document has the query
  documentName-         gives the document name
  debug-                dumps original text of the file
  
# OOD
## OOD1
Class Stoplist
Finding Attributes:
  stoplist-             contains all of the stop words
Finding Services:
  create-               create(String filename)
                        Initializes a stoplist from the filename
  getStoplist-          getStoplist()
                        return the the stoplist as an arraylist

Class InvertedIndex
Finding Attributes:
  stoplist-             list of all stop words
  docIndex-             hashmap of query and documents that had the query
  containIn-            hashset of documents that had the query
  documents-            list of all documents
Finding Services:
  create-               create(String filename)
                        initializes an inverted index
  addDocument-          addDocument(Document d)
                        adds a document to the list of documents and gets rid of stop words
  singleWordQuery-      singleWordQuery(String query, boolean debug)
                        Puts every document that contained the query into a hashset, outputs how many
                        and which documents had the query, and if the debug is true, outputs the document's 
                        contents                       
  multiWordQuery-       multiWordQuery(String query, boolean debug)
                        Puts every document that contained the phrase into a hashset, outputs how many
                        and which documents had the phrase, and if the debug is true, outputs the document's 
                        contents
  debug-                debug()
                        dumps all information from the invertedindex

Class Document
Finding Attributes:
  name-                 name of the document
  originalText-         list of the words from the file with punctuation and spaces
  editedText-           list of the words from the file without punctuation and spaces
Finding Services:
  create-               create(String filename)
                        initializes a document from filename, and creates an arraylist that has
                        the original contents of the document and one without the punctuaction and stopwords
  get rid of stop words-ridStopWords(Stoplist stoplist)
                        Takes the editedText of the document and removes all stopwords from being searched
  hasQuery-             hasQuery(String query)
                        checks if the document has the query
  has (phrase) query-   hasQuery(String[] list)
                        checks if the document has the phrase
  documentName-         documentName()
                        returns the document name
  debug-                debug()
                        dumps original text of the file
                        
Class CLI
Finding Attributes:
  debug-                boolean of whether documents dump their contents or not
  invertedindex-        stores the invertedindex
Finding Services:
  process-              process(String[] args)
                        Processes the user's commands, inputed queries, and times how long the invertedindex took
  main-                 main(String[] args)
                        Runs the program

## OOD2
Class Stoplist
Finding Attributes:
  stoplist-             ArrayList<String> stoplist
Finding Services:
  create-               void Stoplist(String filename)
                        stoplist = new ArrayList<?();
                        Scanner file = new Scanner(new File (filename));
  getStoplist-          ArrayList<String> getStoplist()
                        return stoplist

Class InvertedIndex
Finding Attributes:
  stoplist-             Stoplist
  docIndex-             HashMap<String, HashSet<String>> docIndex
  containIn-            HashSet<String> containIn
  documents-            ArrayList<String> documents
Finding Services:
  create-               create(String filename)
                        docIndex = new HashMap<>()
                        stoplist = new Stoplist(filename)
                        containIn = new HashSet<>()
                        documents = new ArrayList<>()
  addDocument-          void addDocument(Document d)
                        d.ridStopWords(stoplist)
                        documents.add(d)
  singleWordQuery-      String singleWordQuery(String query, boolean debug)
                        query = query.toLowerCase()
                        containIn = new HashSet<>()
                        StringBuilder contents = new StringBuilder()
                        if (!(containIn.size() == 0))
                            docIndex.put(query,containIn)
                        for(String s1 : containIn)
                            s.append(s1+ ", ")
                        return s.toString() + "\n" + contents.toString()
  multiWordQuery-       String multiWordQuery(String query, boolean debug)
                        String [] list = {}
                        list = query.toLowerCase().split(" ")
                        containIn = new HashSet<>()
                        StringBuilder contents = new StringBuilder()
                        if (!(containIn.size() == 0))
                            docIndex.put(query,containIn)
                        for(String s1 : containIn)
                            s.append(s1+ ", ")
                        return s.toString() + "\n" + contents.toString()
  debug-                void debug()
                        System.out.println("The inverted index contains " + docIndex)

Class Document
Finding Attributes:
  name-                 String name
  originalText-         ArrayList<String> originalText
  editedText-           ArrayList<String> editedText
Finding Services:
  create-               void Document(String filename)
                        name = fileName
                        editedText = new ArrayList<>()
                        originalText = new ArrayList<>()
                        Scanner file = new Scanner(new File(name))
                        int i = 0
                        String s = ""
                        String [] temp = {}
                            originalText.add(file.nextLine())
                            s = originalText.get(i).toLowerCase()
                            temp = s.replaceAll("[^a-zA-Z ]", "").split(" ");
                            Collections.addAll(editedText, temp);
                            i++;
  get rid of stop words-void ridStopWords(Stoplist stoplist)
                        ArrayList<String> stop = stoplist.getStoplist()
                        for(String s : stop)
                            editedText.remove(s)
  hasQuery-             boolean hasQuery(String query)
                        return editedText.contains(query)
  has (phrase) query-   boolean hasQuery(String[] list)
                        for (String s : list)
                             if (!this.hasQuery(s))
                                  return false
                        return true
  documentName-         String documentName()
                        returns name
  debug-                String debug()
                        StringBuilder s = new StringBuilder(name + " contains: \n")
                        for (String s1 : originalText)
                              s.append(s1)
                        return s.toString()
                        
Class CLI
Finding Attributes:
  debug-                boolean debug
  invertedindex-        InvertedIndex ii 
Finding Services:
  process-              void process(String[] args)
                        debug = false
                        if (args.length > 1)
                              if (args[0].equals("-d"))
                                    debug = true
                                    ii = new InvertedIndex(args[1])
                                    for (int i = 2; i < args.length; i++)
                                        Document d = new Document(args[i])
                                        ii.addDocument(d)
                               else
                                    ii = new InvertedIndex(args[0])
                                    for (int i = 1; i < args.length; i++)
                                        Document d = new Document(args[i])
                                        ii.addDocument(d)
                                Scanner scan = new Scanner (System.in)
                                String take = ""
                                while (!taken.equals("-stop"))
                                    taken = scan.nextLine()
                        else
                              System.out.println(Error message)
  main-                 void main(String[] args)
                        CLI cli = new CLI()
                        cli.process(args)

# Use Cases
Input: java CLI stoplist fun.txt
       stoplist contains "the"
       fun.txt contains "Java is the best coding language"
       query is "Java"
Expected Output: fun.txt
       
Input: java CLI -d stoplist good.txt maybe.txt
       stoplist contains ""
       good.txt contains "good times"
       maybe.txt contains "so call me maybe"
       query is "maybe"
       
Expected Output: maybe.txt
                 so call me maybe
