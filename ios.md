#iOS

```
//Hide Keyboard
textField.resignFirstResponder() 
	
	
//hide keyboard on click outside of input box (text field)
override func touchesBegan(touches: NSSet!, withEvent event: UIEvent!) {
	self.view.endEditing(true)
}

IBOutlet //Ties to a display element in Storyboard such as a table view or label

IBAciton //Ties to an input element in Storyboard such as a button


UITableView
Delegate
TableView(delegate?).reloadData()
```    
    