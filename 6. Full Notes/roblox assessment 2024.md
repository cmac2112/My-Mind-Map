
2024-11-02 14:02

Status:

Tags:

# roblox assessment 2024


There are some lamps placed on a coordinate line. Each of these lamps illuminates some space around it within a given radius. You are given the coordinates of the lamps on the line, and the effective radius of each of the lamps' light.

In other words, you are given a two-dimensional array `lamps`, where `lamps[i]` contains information about the `ith` lamp. `lamps[i][0]` is an integer representing the lamp's coordinate, and `lamps[i][1]` is a positive integer representing the effective radius of the `ith` lamp. That means that the `ith` lamp illuminates everything in a range from `lamps[i][0] - lamps[i][1]` to `lamps[i][0] + lamps[i][1]` inclusive.

Your task is to find the coordinate of the point that is illuminated by the highest number of lamps. In case of a tie, return the point among them with the minimal possible coordinate.

gpt answer
```
def solution(lamps):

    #find the number that is less than all instances of light

    #position determines how far a light can go, so use position

    #find all possible areas lit up by lamp for each lamp

    #then count and return highest

    #add and subtract from the position to get all lit up areas for a given lamp

    event = []

    for cord, radius in lamps:

        event.append((cord - radius, "start"))

        event.append((cord + radius + 1, "end"))

    event.sort(key=lambda x: (x[0], x[1] == "end"))

    max_count = 0

    current_count = 0

    best = None

    for cord, event_type in event:

        if event_type == "start":

            current_count += 1

        else:

            current_count -= 1

        if current_count > max_count:

            max_count = current_count

            best = cord

        elif current_count == max_count and best is not None:

            best = min(best, cord)

    return best
```




![[Pasted image 20241102140812.png]]
![[Pasted image 20241102140846.png]]
```

def solution(matrix, radius):

  

    rows = len(matrix)

    cols = len(matrix[0])

    max_sum = float('-inf')

    def bounds(x,y):

        return 0 <= x < rows and 0 <= y < cols

    for centerx in range(rows):

        for centery in range(cols):

            rhomb_sum = 0

            valid_rhomb_area = True

            for dx in range(-radius + 1, radius):

                for dy in range(-radius + 1 + abs(dx), radius - abs(dx)):

                    cellx, celly = centerx + dx, centery + dy

                    if bounds(cellx, celly):

                        rhomb_sum += matrix[cellx][celly]

                    else:

                        valid_rhomb_area = False

                        break

                if not valid_rhomb_area:

                    break

            if valid_rhomb_area:

                max_sum = max(max_sum, rhomb_sum)

    return max_sum
    ```