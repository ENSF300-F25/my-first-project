"# my-first-project" 

def menu_option():
   
     '''Prints menu options and prompts user to select an option to manipulate csv data accordingly
    
    Returns:
        user_input (str): a valid input choosing a specific option
    '''

     # Prints menu options
  print(f"\nChoose one of the following options: ")
  print(f"\t1. Finding the max (Highest Rank, Most Popular Genre, Highest Sale Numbers)")
  print(f"\t2. Finding the min (Lowest Rank, Least Popular Genre, Lowest Sale Numbers)")
  print(f"\t3. Finding the average (Average Ranking, Average Amount of Games in All Genres, Average Sale Numbers)")
  print(f"\t0. Return to main menu.")

     # Prompts user for an input
  user_input = input(">> ")

     # Checking for invalid inputs
  if (user_input != "0" and user_input != "1" and user_input != "2" and user_input != "3"):
      error_massage()         # Calls error message function
      return menu_option()    # Recalls this function until a correct valid input
  else:
      return user_input       # Returns the user selection as a string

def aquiring_data_to_useable_form(plateform,rank,sale,genre):
          
      '''Pulls the correct information according to user selection of the platform
    
    Parameters:
      plateform (str): a valid plateform
      rank (nested lst): a list containing multiple list containing [Rank,Name,Platform] of all games in data
      sale (nested lst): a list containing multiple list containing [Platform,NA_Sales,EU_Sales,JP_Sales,Other_Sales,Global_Sales] of all games in data
      genre (nested lst): a list containing multiple list containing [Platform,Year,Genre,Publisher] of all games in data

    Returns:
        list: [all_ranks,na_sales,eu_sales,jp_sales,other_sales,global_sales, all_genre]
            list contains relevant information about the specific user platform
  '''
    
    # Establishing all needed lists to hold relevant information
  all_ranks = []
  na_sales = []
  eu_sales = []
  jp_sales = []
  other_sales = []
  global_sales = []
  all_genre = [] 
    
    # loops in all items checking for the user plateform and extracts revelant information
  for i in range(len(rank)):
          # checking if the plateform is the same as the user choice
      if (rank[i][2] == plateform):
          # adds ranking of game 
          all_ranks += [int(rank[i][0])]
        # checking if the plateform is the same as the user choice
        if (sale[i][0] == plateform):
            # adds sale data
          na_sales += [float(sale[i][1])]
            eu_sales += [float(sale[i][2])]
            jp_sales += [float(sale[i][3])]
            other_sales += [float(sale[i][4])]
            global_sales += [float(sale[i][5])]

        # checking if the plateform is the same as the user choice
   if (genre[i][0] == plateform):
            # adds genre to list
            all_genre += [genre[i][2]]
    
    # returns all relevant information
   return [all_ranks,na_sales,eu_sales,jp_sales,other_sales,global_sales, all_genre]

def get_max(data):
      
      '''Uses all relevant information to find max rank, sale numbers and most popular genre
    
     Parameters:
        data (lst): Contains all relevant information to calculate max
            [all_ranks,na_sales,eu_sales,jp_sales,other_sales,global_sales, all_genre]   
    
      Returns:
        list: [highest rank, Most sales (na),Most sales (eu) ,Most sales (jp), Most sales (other), Most sales (globally), how many times each genre appeared]
'''

      # declare all nessesary variables
initial_genre_list = [0,0,0,0,0,0,0,0,0,0,0,0]
    
      # converting list into numpy arrays
rank_array = np.array(data[0])
na_sales_array = np.array(data[1])
eu_sales_array = np.array(data[2])
jp_sales_array = np.array(data[3])
other_sales_array = np.array(data[4])
global_sales_array = np.array(data[5])

      # loops to count how many times each genre is present
for j in data[6]:
  for k in range(len(gi.ALL_GENRE)):
    if j == gi.ALL_GENRE[k]:
      initial_genre_list[k] += 1

    
def get_min(data):
    
    '''Uses all relevant information to find the lowest rank, the lowest sale numbers and least popular genre
    
     Parameters:
        data (lst): Contains all relevant information to calculate min
            [all_ranks,na_sales,eu_sales,jp_sales,other_sales,global_sales, all_genre]   
    
     Returns:
        list: [Lowest rank, Least sales (na),Least sales (eu) ,Least sales (jp), Least sales (other), Least sales (globally), how many times each genre appeared]
    '''
    
      # declare all nessesary variables
   initial_genre_list = [0,0,0,0,0,0,0,0,0,0,0,0]
    
      # converting list into numpy arrays
rank_array = np.array(data[0])
na_sales_array = np.array(data[1])
eu_sales_array = np.array(data[2])
jp_sales_array = np.array(data[3])
other_sales_array = np.array(data[4])
global_sales_array = np.array(data[5])


      # loops to count how many times each genre is present
for genre_in_list in data[6]:
  for specific_genre_index in range(len(gi.ALL_GENRE)):
    if genre_in_list == gi.ALL_GENRE[specific_genre_index]:     # checking to see which genre was found 
      initial_genre_list[specific_genre_index] += 1           # counting the number of times each genre was found
    
return [rank_array.max(), na_sales_array.min(),eu_sales_array.min(),jp_sales_array.min(),other_sales_array.min(), global_sales_array.min(), initial_genre_list]

    
    
def print_min_values(plateform,info,rank_list,sale_list,genre_list):
    
    '''Find the rest of the nessesary information and extra details to print the information to the user in a nice format
    
     Parameters:
    plateform (str): a valid plateform
    info (str): a list containing [Lowest rank, Least sales (na),Least sales (eu) ,Least sales (jp), Least sales (other), Least sales (globally), average games        per genre]
    rank (nested lst): a list containing multiple list containing [Rank,Name,Platform] of all games in data
    sale (nested lst): a list containing multiple list containing [Platform,NA_Sales,EU_Sales,JP_Sales,Other_Sales,Global_Sales] of all games in data
    genre (nested lst): a list containing multiple list containing [Platform,Year,Genre,Publisher] of all games in data
    
    '''


     # Declaring nessesary variables
  num_which_info_is_found_at = [0,0,0,0,0,0,0]
    
     # finding the lowest number of games for a genre 
  value_of_min_genre = min(info[6])
  index_where_min_genre_is_at = 0
    
     # Loop to find index where important information is found
  for i in range (len(rank_list)):
    if rank_list[i][0] == info[0]:
      num_which_info_is_found_at[0] = i
        
   for j in range(1,6):
      if float(sale_list[i][j]) == info[j]:
         num_which_info_is_found_at[j] = i

   for k,l in enumerate(info[6]):
         if l == value_of_min_genre:
            index_where_min_genre_is_at = k


     # Printing all minimum data
  print(f"\nMinimum Data:")
  print(f"The lowest ranking video game in terms of sales is {rank_list[num_which_info_is_found_at[0]][1]} ranking {info[0]} out of 16600")
    
     # Printing sale numbers while checking if the number is too low 
  for k in range(1,6):
    if info[k] == 0:
      print(f"The lowest selling video game {gi.REGION_PRINT[k-1]} for the {plateform} is '{rank_list[num_which_info_is_found_at[k]][1]}' selling less than 10,000       units")
    else:
        print(f"The lowest selling video game {gi.REGION_PRINT[k-1]} for the {plateform} is '{rank_list[num_which_info_is_found_at[k]][1]}' selling {info[k]}               million units.")
    
   print(f"The least popular genre is {gi.ALL_GENRE[index_where_min_genre_is_at]} having {value_of_min_genre} games.")
   print()
    
