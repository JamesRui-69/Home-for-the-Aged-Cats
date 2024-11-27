# Home-for-the-Aged-Cats
This C++ program gamifies heap operations by letting users manage the ages of cats in a shelter. It supports inserting ages into a Max-Heap, converting to a Min-Heap, heapifying random ages, and deleting specific ages. Featuring colorful visuals, animated messages, and a history log, it blends fun and learning about heap data structures.

}

// Function to delete an element from the heap
void deleteFromHeap(vector<int>& heap, int age) {
    auto it = find(heap.begin(), heap.end(), age);
    if (it != heap.end()) {
        cout << RED << "Deleting age " << age << " from the heap." << RESET << endl;
        heap.erase(it);
        make_heap(heap.begin(), heap.end());
        displayHeap(heap);
        history.push_back("Deleted age " + to_string(age) + " from the heap.");
        if (!minHeap.empty()) {
            convertToMinHeap(maxHeap); // Update the min heap after deletion
        }
    } else {
        cout << RED << "Age " << age << " not found in the heap." << RESET << endl;
    }
}

int main() {
    int choice, age;
    string welcomeMessage = "Hello! Welcome, it's your first day as a vet \n" "Your task is to manage the ages of the pets in the shelter.\n" "Let's get started!\n";
    for (char c : welcomeMessage) {
        cout << c << flush;
        this_thread::sleep_for(chrono::milliseconds(25));
    }

    while (true) {
        cout << MAGENTA << "\nHome for the aged Cats at the shelter (CATS):\n" << RESET;
        cout << "1. Insert age of a cat\n";
        cout << "2. Convert Max-Heap to Min-Heap\n";
        cout << "3. Heapify random ages into a Max-Heap\n";
        cout << "4. Remove a naughty cat\n";
        cout << "5. Finish your duty and recap\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cout << " \n";
        cin >> choice;

        switch (choice) {
            case 1:
                while (true) {
                    cout << "Enter age to insert (or -1 to stop): ";
                    cin >> age;
                    if (age == -1) break;
                    insertMaxHeap(maxHeap, age);
                    userInputAges.push_back(age); // Store the user input
                }
                break;
            case 2:
                convertToMinHeap(maxHeap);
                break;
