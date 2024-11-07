let
    Source = Csv.Document(File.Contents("C:\Users\admin\Desktop\powerbi\labs\03-model-data\data\Addresses.csv"),[Delimiter=",", Columns=5, Encoding=65001, QuoteStyle=QuoteStyle.None]),
    #"En-têtes promus" = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    #"Type modifié" = Table.TransformColumnTypes(#"En-têtes promus",{{"AddressID", type text},{"Street", type text}, {"City", type text}, {"PostalCode", type text}, {"Region", type text}}),
    //Script de modification de OOO par 000
    #"Remplacé par 000" = Table.TransformColumns(#"Type modifié", 
    List.Transform(
    Table.ColumnNames(#"Type modifié"), 
    (colname) => 
    {colname, each Text.Replace(_, "OOO", "000")})),
    #"Colonne conditionnelle ajoutée" = Table.AddColumn(#"Remplacé par 000", "ValidationCodePostal", each if Value.Is(Value.FromText([PostalCode]), type number) and (Text.Length([PostalCode]) = 5) then "Valide" else "No Valide"),
    #"Valeur remplacée" = Table.ReplaceValue(#"Colonne conditionnelle ajoutée","","Toulouse",Replacer.ReplaceValue,{"City"})
in
    #"Valeur remplacée"