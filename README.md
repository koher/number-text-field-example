# NumberTextFieldExample

```swift
import UIKit

class ViewController: UIViewController {
    @IBOutlet var textField: UITextField!
    @IBOutlet var sendButton: UIButton!

    override func viewDidLoad() {
        super.viewDidLoad()

        textField.addTarget(self, action: #selector(textFieldDidChangeText(_:)), for: .editingChanged)
    }

    @IBAction func pressSendButton(_ button: UIButton) {
        // Forced unwrapping here because `text` is always a valid number becuase of UI restrictions
        let number = Int(textField.text!)!
        print(number)
    }

    @objc func textFieldDidChangeText(_ textField: UITextField) {
        sendButton.isEnabled = !(textField.text?.isEmpty ?? true)
    }
}

extension ViewController: UITextFieldDelegate {
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        if string.isEmpty { return true }
        if (textField.text ?? "") == "" && string.first! == "0" { return false }
        return Int(string) != nil
    }
}
```
