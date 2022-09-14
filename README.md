# Test-

Refactoring


```Swift

import UIKit

class TodoListViewController: UITableViewController {
    
    private var items: [String]? = nil
    
    override func viewDidLoad() {
        super.viewDidLoad()
        loadItems()
    }
    
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return items?.count ?? 0
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "ToDoItemCell", for: indexPath)
        cell.textLabel?.text = items?[indexPath.row]
        return cell
    }
    
    override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        if tableView.cellForRow(at: indexPath)?.accessoryType == .checkmark {
           tableView.cellForRow(at: indexPath)?.accessoryType = .none
        } else {
            tableView.cellForRow(at: indexPath)?.accessoryType = .checkmark
        }
    }
    
    @IBAction func addButtonPressed(_ sender: UIBarButtonItem) {
        var textField = UITextField()
        let alert = UIAlertController(title: "Add New Item", message: "", preferredStyle: .alert)
        let action = UIAlertAction(title: "Add Item", style: .default) { (action) in
            self.items?.append(textField.text!)
        }
        alert.addTextField { (alertTextField) in
            alertTextField.placeholder = "Create new item"
            textField = alertTextField
        }
        alert.addAction(action)
        present(alert, animated: true, completion: nil)
        self.tableView.reloadData()
        self.saveItems()
    }
    
    

    
    private func loadItems() {
        // Suppose it's a DB query here instead
        DispatchQueue.main.asyncAfter(deadline: .now() + 1.0) {
            self.items = [
               "Buy Milk",
               "Buy Eggs",
               "Pass a Tech Interview",
               "Create an App",
               "Refactor the App",
               "Read a book",
               "Cook some food",
               "Pay the rent",
               "Call Bob",
               "Go out",
               "Take the dog to the vet",
               "Get a job"
           ]
        }
    }
    
    private func saveItems() {
        //...
    }

}
```
