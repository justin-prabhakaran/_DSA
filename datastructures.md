### Linked List
two pointer linked list (head,tail)
```java
class Main{
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.insert(new LinkedList.Node(1));
        list.insert(new LinkedList.Node(2));
        list.insert(new LinkedList.Node(3));
        list.print();
        list.printRev();

        list.print();
        list.insert(new LinkedList.Node(4),1);
        list.print();

        list.deleteAt(0);
        list.print();

        System.out.println(list.elementAt(0));
        System.out.println(list.elementAt(1));

        System.out.println(list.indexOf(4));
        System.out.println(list.indexOf(1));

        System.out.println(list.contains(4));
        System.out.println(list.contains(1));

    }
}

 public class LinkedList {

    static class Node {
         private final int val;
         private Node prev;
         private Node next;

         Node(int val) {
             this.val = val;
         }
     }

    private Node head;
    private Node tail;
    private int size;

    public boolean contains(int element){
        return indexOf(element) != -1;
    }
     public int indexOf(int element){
         Node start = head, end = tail;
         int sindex = 0, eindex = size;
         while (start != null && end != null){
             if(start.val == element){
                 return sindex;
             }else if(end.val == element){
                 return eindex;
             }
             sindex++;
             eindex--;
             start = start.next;
             end = end.prev;
         }

         return -1;
     }


    public int elementAt(int index){
        if(index < 0 || index > size){
            throw new IndexOutOfBoundsException("Invalid index");
        }
        else if(index == 0){
            return head.val;
        }


        else if(index == size){
            return tail.val;
        }
        else{
            Node temp ;
            if(index > size / 2){
                temp = tail;
                for(int i=size-1;i > index;i--){
                    temp = temp.prev;
                }
            }else{
                temp = head;
                for(int i=0;i<index;i++){
                    temp = temp.next;
                }
            }

            return temp.val;

        }

    }

    public void deleteAt(int index){
        if(index < 0 || index > size){
            throw new IndexOutOfBoundsException("Invalid index");
        }
        else if(index == 0){
            head = head.next;
            head.prev = null;
        }else if(index == size){
            tail = tail.prev;
            tail.next= null;
        }
        else{
            Node temp;
            if(index > size / 2){
                temp = tail;
                for(int i=size-1;i > index;i--){
                    temp = temp.prev;
                }
            }else{
                temp = head;
                for(int i=0;i< index;i++){
                    temp = temp.next;
                }
            }
            temp.prev.next = temp.next;
            temp.next.prev = temp.prev;

        }
        size--;
    }


    public void insert(Node node){
        if(head == null){
            head = node;
            tail = node;
            return;
        }
        Node temp = head;
        while (head.next != null){
            head = head.next;
        }
        head.next = node;
        node.prev = head;
        tail = node;
        head = temp;
        size++;
    }

    public void insert(Node node, int index){
        if(index <0 || index > size){
            throw new IndexOutOfBoundsException("index not valid");
        }
        if(index == 0 ){
           if(head == null){
               head = node;
               tail = node;
           }else{
               node.next = head;
               head.prev = node;
               head = node;
           }
        }
        else if(index == size){
            insert(node);
        }
        else{
            Node temp;
            if(index > size / 2 ){
                temp = tail;
                for(int i = size-1;i > index;i--){
                    temp = temp.prev;
                }
            }else{
                temp = head;
                for(int i=0;i<index-1;i++){
                    temp = temp.next;
                }
            }

            node.next = temp.next;
            node.prev = temp;
            if(node.next != null){
                node.next.prev = node;
            }
            temp.next = node;
        }
        size++;
    }

    public void print(){
        Node temp = head;
        while (temp != null){
            System.out.print(temp.val + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    public void printRev(){
        Node temp = tail;
        while (temp != null){
            System.out.print(temp.val + " ");
            temp = temp.prev;
        }
        System.out.println();
    }

}
```
