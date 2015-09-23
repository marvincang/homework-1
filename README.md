# homework-1/
**
 * My implementation of a SinglyLinkedList
 *
 * @author Marvin Cangcianno
 * @version 1.0
 */
 
public class SinglyLinkedList<T> implements LinkedListInterface<T> {

    // Do not add new instance variables.
    private LinkedListNode<T> head;
    private int size;

    @Override
    public void addAtIndex(int index, T data) {
        if (index < 0 || index > size)
            throw new IndexOutOfBoundsException("Can't add data into this index.");
        
        if (data == null)
            throw new IllegalArgumentException("Can't insert null value into the node.");
            
        if (index == 0){
            head = new LinkedListNode<>(data);
            size++;
        }
        else{
            LinkedListNode<T> temp = head;
            for (int i = 0; i < index - 1; i++)
                temp = temp.getNext();
            LinkedListNode<T> newNode = new LinkedListNode<>(data, temp.getNext());
            temp.setNext(newNode);
            size++;
        }
    }

    @Override
    public T get(int index) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("Index should be between 0 and the list's length.");
        
        if (index == 0)
            return head.getData();
        else{    
            LinkedListNode<T> temp = head;
            for (int i = 0; i < index; i++){
                temp = temp.getNext();
            }
            return temp.getData();
        }
    }

    @Override
    public T removeAtIndex(int index) {
        if (index < 0 || index >= size)
            throw new IndexOutOfBoundsException("Index should be between 0 and the list's length.");
        
        if (index == 0){
            T data = head.getData();
            head.setNext(head.getNext());
            size--;
            return data;
        }
        else{
            LinkedListNode<T> temp = head;
            for (int i = 0; i < index - 1; i++){
                temp = temp.getNext();
            }
            T data = temp.getNext().getData();
            temp.setNext(temp.getNext().getNext());
            size--;
            return data;
        }
    }

    @Override
    public void addToFront(T data) {
        if (data == null)
            throw new IllegalArgumentException("Can't insert null value into the node.");
        head = new LinkedListNode<>(data, head);
        size++;
    }

    @Override
    public void addToBack(T data) {
        if (data == null)
            throw new IllegalArgumentException("Can't insert null value into the node.");
        
        if (size == 0){
            head = new LinkedListNode<>(data);
            size++;
        }
        else{   
            LinkedListNode<T> temp = head;
            while (temp.getNext() != null){
                temp = temp.getNext();
            }
            temp.setNext(new LinkedListNode<>(data));
            size++;
        }
    }

    @Override
    public T removeFromFront() {
        if (size == 0)
            return null;
        
        T data = head.getData();
        head.setNext(head.getNext());
        size--;
        return data;
    }

    @Override
    public T removeFromBack() {
        if (size == 0)
            return null;
        
        LinkedListNode<T> temp = head;
        while (temp.getNext().getNext() != null){
            temp = temp.getNext();
        }
        T data = temp.getData();
        temp.setNext(null);
        size--;
        return data;
    }

    @Override
    public int removeFirstOccurrence(T data) {
        if (data == null)
            throw new IllegalArgumentException("Can't remove since data is null.");
        
        if (head.getData().equals(data)){
            head.setNext(head.getNext());
            size--;
            return 0;
        }
        LinkedListNode<T> temp = head;
        int index = 0;
        boolean b = false;
            
        while (temp.getNext() != null && b != true){
            if (temp.getNext().getData().equals(data))
                b = true;
            else{
                temp = temp.getNext();
                index++;
            }
        }
        index++;
        temp.setNext(temp.getNext().getNext());
        size--;
        return index;
    }

    @Override
    public Object[] toArray() {
        Object[] newArray = new Object[size];
        LinkedListNode<T> temp = head;
        for (int i = 0; i < size; i++){
            newArray[i] = temp.getData();
            temp = temp.getNext();
        }
        return newArray;
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public int size() {
        return size;
    }

    @Override
    public void clear() {
        head = null;
        size = 0;
    }

    @Override
    public LinkedListNode<T> getHead() {
        // DO NOT MODIFY!
        return head;
    }
}
