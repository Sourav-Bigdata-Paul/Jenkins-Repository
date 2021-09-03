class Qentry{
	@BeanProperty
	var v: Int = _
	@BeanProperty
	var dist: Int = _
}
}
def getMinDiceThrows(move: Array[Int], n: Int): Int ={
	val visited = Array.ofDim[Int](n)
	val q = Queue[Int]()
	var qe = new Qentry()
	qe.v = 0
	qe.dist = 0

	visited(0) = 1
	q.enqueue(qe)

	val loopBreak = Breaks

	loopBreak.breakable{
		while(q.nonEmpty){
			qe = q.dequeue
			val v = qe.v

			if(v == n-1)
				loopBreak.break

			var j = v+1

			while(j <= v+6 && j < n){
				if(visited(j) == 0){
					val a = new Qentry()
					a.dist = qe.dist + 1
					visited(i) = 1

					if(move(j) != -1)
						a.v = move(j)
					else
						a.v = j

					q.enqueue(a)
				}
				j += 1
			}
		}
	}
	return qe.dist	
}

def main(args: Array[String]){
    val N = 30
    val moves = Array.ofDim[Int](N)
    for (i <- 0 until N by 1)
        moves(i) = -1

    // Ladders
    moves(2) = 21
    moves(4) = 7
    moves(10) = 25
    moves(19) = 28

    // Snakes
    moves(26) = 0
    moves(20) = 8
    moves(16) = 3
    moves(18) = 6

   println("Min Dice throws required is " + getMinDiceThrows(moves, N))
}


==================================================================================================================================================================================================


def appearsNBy3(arr: Array[Int], n: Int): Int ={
	var count1 = 0
	var count2 = 0

	var first = Int.MinValue
	var second = Int.MaxValue

	for(i <- 0 until n by 1){

		if(arr(i) == first)
			count1 += 1

		else if(arr(i) == second)
			count2 += 1

		else if(count1 == 0){
			count1 += 1
			first = arr(i)
		}

		else if(count2 == 0){
			count2 += 1
			second = arr(i)
		}

		else{
			count1 -= 1
			count2 -= 1
		}
	}

	count1 = 0
	count2 = 0

	for(i <- 0 until n by 1){
		if(first == arr(i))
			count1 += 1
		if(second == arr(i))
			count2 += 1
	}

	if(count1 > n/2)
		return first

	if(count2 > n/2)
		return second

	return -1
}	

def main(args: Array[String]){
	val arr = Array(1, 2, 3, 1, 1)
    val n = arr.length
    println(appearsNBy3(arr, n))
}    


==================================================================================================================================================================================================
coin change problem

def countWays(arr: Array[Int], m: Int, n: Int){
	val table = Array.fill[Int](n+1)(0)
	table(0) = 1

	for(i <- 0 until m by 1)
		for(j <- arr(i) to n by 1)
			table(j) += table(j-arr(i))

	return table(n)		 
}

def main(args: Array[String]){
	val arr = Array(1, 2, 3)
	val m = arr.length
    val n = 4
    println(countWays(arr, m, n))
}  


==================================================================================================================================================================================================


Consider a game where a player can score 3 or 5 or 10 points in a move. Given a total score n, find number of ways to reach the given score.

Same as above


==================================================================================================================================================================================================


class GFG {
 
    /* Function to find a maximum product of a triplet
   in array of integers of size n */
    static int maxProduct(int arr[], int n) {
        // if size is less than 3, no triplet exists
        if (n < 3) {
            return -1;
        }
 
        // Sort the array in ascending order
        Arrays.sort(arr);
 
        // Return the maximum of product of last three
        // elements and product of first two elements
        // and last element
        return Math.max(arr[0] * arr[1] * arr[n - 1],
                arr[n - 1] * arr[n - 2] * arr[n - 3]);
    }
 
// Driver program to test above functions
    public static void main(String[] args) {
        int arr[] = {-10, -3, 5, 6, -20};
        int n = arr.length;
 
        int max = maxProduct(arr, n);
 
        if (max == -1) {
            System.out.println("No Triplet Exists");
        } else {
            System.out.println("Maximum product is " + max);
        }
 
    }
}
