Subject: Request for Approval of Work-from-Home Assets Reimbursement

Dear [HR Representative's Name],

I hope this email finds you well. I am writing to seek your approval for my work-from-home assets reimbursement request, which has been returned to me as it exceeds the 90-day period from my date of joining.

I kindly request your assistance in processing this reimbursement as it includes essential expenses I incurred to set up a conducive work environment for my role. Please let me know if any additional information or documentation is required to facilitate the approval.

Looking forward to your support on this matter.

Thank you for your time and consideration.

Best regards,
[Your Full Name]
[Your Employee ID, if applicable]
[Your Contact Information]

Feel free to adjust the details to suit your situation.


2/2











ChatGPT can make mistakes. Check impackage com.socgen.laxmihealth.community;

import com.socgen.laxmihealth.community.CommunityController;
import com.socgen.laxmihealth.community.CommunityPost;
import com.socgen.laxmihealth.community.CommunityService;
import com.socgen.laxmihealth.community.PostComment;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import java.util.ArrayList;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.ArgumentMatchers.anyLong;
import static org.mockito.Mockito.*;

public class CommunityControllerTest {

    @InjectMocks
    private CommunityController communityController;

    @Mock
    private CommunityService communityService;

    @BeforeEach
    public void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testGetAllPosts() {
        // Arrange
        List<CommunityPost> posts = new ArrayList<>();
        posts.add(new CommunityPost(1L, "Post 1", "Content 1", null));
        posts.add(new CommunityPost(2L, "Post 2", "Content 2", null));

        when(communityService.getAllPosts()).thenReturn(posts);

        // Act
        ResponseEntity<List<CommunityPost>> response = communityController.getAllPost();

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(2, response.getBody().size());
        verify(communityService, times(1)).getAllPosts();
    }

    @Test
    public void testGetPostById() {
        // Arrange
        long postId = 1L;
        CommunityPost post = new CommunityPost(postId, "Post 1", "Content 1", null);

        when(communityService.getPostById(postId)).thenReturn(post);

        // Act
        ResponseEntity<CommunityPost> response = communityController.getPost(postId);

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(postId, response.getBody().getPostId());
        verify(communityService, times(1)).getPostById(postId);
    }

    @Test
    public void testCreatePost() {
        // Arrange
        CommunityPost newPost = new CommunityPost(null, "New Post", "New Content", null);
        CommunityPost savedPost = new CommunityPost(1L, "New Post", "New Content", null);

        when(communityService.createOrUpdatePost(any(CommunityPost.class))).thenReturn(savedPost);

        // Act
        ResponseEntity<CommunityPost> response = communityController.createPost(newPost);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(savedPost.getPostId(), response.getBody().getPostId());
        verify(communityService, times(1)).createOrUpdatePost(any(CommunityPost.class));
    }

    @Test
    public void testAddComment() {
        // Arrange
        long postId = 1L;
        PostComment comment = new PostComment("This is a comment", null);
        PostComment savedComment = new PostComment("This is a comment", null);

        when(communityService.addComment(any(PostComment.class), anyLong())).thenReturn(savedComment);

        // Act
        ResponseEntity<PostComment> response = communityController.addComment(postId, comment);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(savedComment, response.getBody());
        verify(communityService, times(1)).addComment(any(PostComment.class), anyLong());
    }

    @Test
    public void testTogglePostLike() {
        // Arrange
        long postId = 1L;

        // Act
        ResponseEntity<Void> response = communityController.togglePostLike(postId);

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        verify(communityService, times(1)).togglePostLike(postId);
    }
}










package com.socgen.laxmihealth.workout;

import com.socgen.laxmihealth.workout.Workout;
import com.socgen.laxmihealth.workout.WorkoutController;
import com.socgen.laxmihealth.workout.WorkoutService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.ArgumentMatchers.anyLong;
import static org.mockito.Mockito.*;

public class WorkoutControllerTest {

    @InjectMocks
    private WorkoutController workoutController;

    @Mock
    private WorkoutService workoutService;

    @BeforeEach
    public void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testGetAllWorkouts() {
        // Arrange
        List<Workout> workouts = new ArrayList<>();
        workouts.add(new Workout(1L, new Date(), new Date(), null));
        workouts.add(new Workout(2L, new Date(), new Date(), null));

        when(workoutService.getAllWorkouts()).thenReturn(workouts);

        // Act
        ResponseEntity<List<Workout>> response = workoutController.getAllWorkouts();

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(2, response.getBody().size());
        verify(workoutService, times(1)).getAllWorkouts();
    }

    @Test
    public void testGetWorkoutById() {
        // Arrange
        long workoutId = 1L;
        Workout workout = new Workout(workoutId, new Date(), new Date(), null);

        when(workoutService.getWorkoutById(workoutId)).thenReturn(workout);

        // Act
        ResponseEntity<Workout> response = workoutController.getWorkoutById(workoutId);

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(workoutId, response.getBody().getWorkoutId());
        verify(workoutService, times(1)).getWorkoutById(workoutId);
    }

    @Test
    public void testCreateWorkout() {
        // Arrange
        Workout workout = new Workout(null, new Date(), new Date(), null);
        Workout savedWorkout = new Workout(1L, new Date(), new Date(), null);

        when(workoutService.createorUpdateWorkout(any(Workout.class))).thenReturn(savedWorkout);

        // Act
        ResponseEntity<Workout> response = workoutController.createWorkout(workout);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(savedWorkout.getWorkoutId(), response.getBody().getWorkoutId());
        verify(workoutService, times(1)).createorUpdateWorkout(any(Workout.class));
    }

    @Test
    public void testAddWorkoutExercise() {
        // Arrange
        long workoutId = 1L;
        long exerciseId = 1L;
        List<ExerciseSet> exercises = new ArrayList<>();
        exercises.add(new ExerciseSet(exerciseId, workoutId));

        Workout updatedWorkout = new Workout(workoutId, new Date(), new Date(), exercises);

        when(workoutService.addExerciseToWorkout(anyLong(), anyLong(), any(List.class))).thenReturn(updatedWorkout);

        // Act
        ResponseEntity<Workout> response = workoutController.addWorkoutExercise(workoutId, exerciseId, exercises);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(workoutId, response.getBody().getWorkoutId());
        verify(workoutService, times(1)).addExerciseToWorkout(workoutId, exerciseId, exercises);
    }
}













package com.socgen.laxmihealth.workout.exercise;

import com.socgen.laxmihealth.workout.exercise.Exercise;
import com.socgen.laxmihealth.workout.exercise.ExerciseRepository;
import com.socgen.laxmihealth.workout.exercise.ExerciseService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

public class ExerciseServiceTest {

    @InjectMocks
    private ExerciseService exerciseService;

    @Mock
    private ExerciseRepository exerciseRepository;

    @BeforeEach
    public void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testGetAllExercises() {
        // Arrange
        List<Exercise> exercises = new ArrayList<>();
        exercises.add(new Exercise(1L, "Push Up", "A basic exercise", "Strength"));
        exercises.add(new Exercise(2L, "Squat", "Lower body exercise", "Strength"));

        when(exerciseRepository.findAll()).thenReturn(exercises);

        // Act
        List<Exercise> result = exerciseService.getAllExercises();

        // Assert
        assertEquals(2, result.size());
        verify(exerciseRepository, times(1)).findAll();
    }

    @Test
    public void testGetExerciseById() {
        // Arrange
        long exerciseId = 1L;
        Exercise exercise = new Exercise(exerciseId, "Push Up", "A basic exercise", "Strength");

        when(exerciseRepository.findById(exerciseId)).thenReturn(Optional.of(exercise));

        // Act
        Exercise result = exerciseService.getExerciseById(exerciseId);

        // Assert
        assertEquals(exerciseId, result.getExerciseId());
        verify(exerciseRepository, times(1)).findById(exerciseId);
    }

    @Test
    public void testGetExerciseById_NotFound() {
        // Arrange
        long exerciseId = 1L;

        when(exerciseRepository.findById(exerciseId)).thenReturn(Optional.empty());

        // Act & Assert
        assertThrows(ObjectNotFoundException.class, () -> exerciseService.getExerciseById(exerciseId));
        verify(exerciseRepository, times(1)).findById(exerciseId);
    }

    @Test
    public void testCreateExercise() {
        // Arrange
        Exercise exercise = new Exercise(null, "Lunge", "Lower body exercise", "Strength");
        Exercise savedExercise = new Exercise(1L, "Lunge", "Lower body exercise", "Strength");

        when(exerciseRepository.save(any(Exercise.class))).thenReturn(savedExercise);

        // Act
        Exercise result = exerciseService.createExercise(exercise);

        // Assert
        assertEquals(savedExercise.getExerciseId(), result.getExerciseId());
        verify(exerciseRepository, times(1)).save(any(Exercise.class));
    }
}








package com.socgen.laxmihealth.workout.exercise;

import com.socgen.laxmihealth.workout.exercise.ExerciseController;
import com.socgen.laxmihealth.workout.exercise.ExerciseService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import java.util.ArrayList;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

public class ExerciseControllerTest {

    @InjectMocks
    private ExerciseController exerciseController;

    @Mock
    private ExerciseService exerciseService;

    @BeforeEach
    public void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    public void testGetExercises() {
        // Arrange
        List<Exercise> exercises = new ArrayList<>();
        exercises.add(new Exercise(1L, "Push Up", "A basic exercise", "Strength"));
        exercises.add(new Exercise(2L, "Squat", "Lower body exercise", "Strength"));

        when(exerciseService.getAllExercises()).thenReturn(exercises);

        // Act
        ResponseEntity<List<Exercise>> response = exerciseController.getExercises();

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(2, response.getBody().size());
        verify(exerciseService, times(1)).getAllExercises();
    }

    @Test
    public void testGetExerciseById() {
        // Arrange
        long exerciseId = 1L;
        Exercise exercise = new Exercise(exerciseId, "Push Up", "A basic exercise", "Strength");

        when(exerciseService.getExerciseById(exerciseId)).thenReturn(exercise);

        // Act
        ResponseEntity<Exercise> response = exerciseController.getExercise(exerciseId);

        // Assert
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(exerciseId, response.getBody().getExerciseId());
        verify(exerciseService, times(1)).getExerciseById(exerciseId);
    }

    @Test
    public void testCreateExercise() {
        // Arrange
        Exercise exercise = new Exercise(null, "Lunge", "Lower body exercise", "Strength");
        Exercise savedExercise = new Exercise(1L, "Lunge", "Lower body exercise", "Strength");

        when(exerciseService.createExercise(any(Exercise.class))).thenReturn(savedExercise);

        // Act
        ResponseEntity<Exercise> response = exerciseController.createExercise(exercise);

        // Assert
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(savedExercise.getExerciseId(), response.getBody().getExerciseId());
        verify(exerciseService, times(1)).createExercise(any(Exercise.class));
    }
}















package com.socgen.laxmihealth.diet;

import com.socgen.laxmihealth.diet.Diet;
import com.socgen.laxmihealth.diet.DietController;
import com.socgen.laxmihealth.diet.DietService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.Mockito.*;

class DietControllerTest {

    @InjectMocks
    private DietController dietController;

    @Mock
    private DietService dietService;

    private Diet diet;

    @BeforeEach
    void setUp() {
        MockitoAnnotations.openMocks(this);
        diet = new Diet();
        diet.setDietId(1L);
        diet.setDietName("Keto Diet");
        diet.setDietType("Low Carb");
        diet.setDietDescription("A low carbohydrate diet");
    }

    @Test
    void testGetAllDiets() {
        List<Diet> diets = new ArrayList<>();
        diets.add(diet);

        when(dietService.getAllDiets()).thenReturn(diets);

        ResponseEntity<List<Diet>> response = dietController.getAllDiets();
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(1, response.getBody().size());
    }

    @Test
    void testGetDietById() {
        when(dietService.getDietById(1L)).thenReturn(Optional.of(diet));

        ResponseEntity<Diet> response = dietController.getDietById(1L);
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(diet, response.getBody());
    }

    @Test
    void testGetDietById_NotFound() {
        when(dietService.getDietById(1L)).thenReturn(Optional.empty());

        ResponseEntity<Diet> response = dietController.getDietById(1L);
        assertEquals(HttpStatus.NOT_FOUND, response.getStatusCode());
    }

    @Test
    void testCreateDiet() {
        when(dietService.createOrUpdateDiet(any(Diet.class))).thenReturn(diet);

        ResponseEntity<Diet> response = dietController.createDiet(diet);
        assertEquals(HttpStatus.CREATED, response.getStatusCode());
        assertEquals(diet, response.getBody());
    }

    @Test
    void testUpdateDiet() {
        when(dietService.createOrUpdateDiet(any(Diet.class))).thenReturn(diet);

        ResponseEntity<Diet> response = dietController.updateDiet(diet);
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals(diet, response.getBody());
    }

    @Test
    void testDeleteDiet() {
        doNothing().when(dietService).deleteDietById(1L);

        ResponseEntity<Void> response = dietController.deleteDiet(1L);
        assertEquals(HttpStatus.NO_CONTENT, response.getStatusCode());
    }
}











package com.socgen.laxmihealth.diet;

import com.fasterxml.jackson.databind.ObjectMapper;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.ResultActions;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;

import java.util.Collections;
import java.util.List;

import static org.mockito.ArgumentMatchers.*;
import static org.mockito.Mockito.*;

@WebMvcTest(controllers = DietController.class)
@AutoConfigureMockMvc
class DietControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private DietService dietService;

    private Diet diet1;

    @BeforeEach
    void setUp() {
        diet1 = new Diet();
        diet1.setDietId(1L);
        diet1.setDietName("Diet 1");
    }

    @Test
    void testGetAllDiets() throws Exception {
        // Mocking service method
        when(dietService.getAllDiets()).thenReturn(Collections.singletonList(diet1));

        // Perform GET request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/diet")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.length()").value(1))
                .andExpect(MockMvcResultMatchers.jsonPath("$[0].dietName").value("Diet 1"));

        // Verify service method invocation
        verify(dietService, times(1)).getAllDiets();
    }

    @Test
    void testGetDietById() throws Exception {
        // Mocking service method
        when(dietService.getDietById(1L)).thenReturn(diet1);

        // Perform GET request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/diet/{dietId}", 1)
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.dietName").value("Diet 1"));

        // Verify service method invocation
        verify(dietService, times(1)).getDietById(1L);
    }

    @Test
    void testCreateDiet() throws Exception {
        // Prepare request body
        ObjectMapper objectMapper = new ObjectMapper();
        String dietJson = objectMapper.writeValueAsString(diet1);

        // Mocking service method
        when(dietService.createOrUpdateDiet(any(Diet.class))).thenReturn(diet1);

        // Perform POST request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.post("/diet")
                .content(dietJson)
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isCreated())
                .andExpect(MockMvcResultMatchers.jsonPath("$.dietName").value("Diet 1"));

        // Verify service method invocation
        verify(dietService, times(1)).createOrUpdateDiet(any(Diet.class));
    }

    @Test
    void testUpdateDiet() throws Exception {
        // Prepare request body
        ObjectMapper objectMapper = new ObjectMapper();
        String dietJson = objectMapper.writeValueAsString(diet1);

        // Mocking service method
        when(dietService.createOrUpdateDiet(any(Diet.class))).thenReturn(diet1);

        // Perform PUT request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.put("/diet")
                .content(dietJson)
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.dietName").value("Diet 1"));

        // Verify service method invocation
        verify(dietService, times(1)).createOrUpdateDiet(any(Diet.class));
    }

    @Test
    void testDeleteDiet() throws Exception {
        // Perform DELETE request
        mockMvc.perform(MockMvcRequestBuilders.delete("/diet/{dietId}", 1)
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(MockMvcResultMatchers.status().isNoContent());

        // Verify service method invocation
        verify(dietService, times(1)).deleteDietById(1L);
    }
}















package com.socgen.laxmihealth.user;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

import com.socgen.laxmihealth.auth.AuthService;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.http.HttpStatus;
import org.springframework.http.MediaType;
import org.springframework.http.ResponseEntity;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import java.util.Arrays;
import java.util.HashSet;
import java.util.List;

@WebMvcTest(UserController.class)
class UserControllerTest {

    @Mock
    private UserService userService;

    @Mock
    private AuthService authService;

    @InjectMocks
    private UserController userController;

    private MockMvc mockMvc;

    private User user1;
    private User user2;

    @BeforeEach
    void setUp() {
        mockMvc = MockMvcBuilders.standaloneSetup(userController).build();

        user1 = new User();
        user1.setId(1L);
        user1.setUsername("user1");
        user1.setUserRoles(new HashSet<>(List.of("ROLE_USER")));

        user2 = new User();
        user2.setId(2L);
        user2.setUsername("user2");
        user2.setUserRoles(new HashSet<>(List.of("ROLE_USER")));
    }

    @Test
    void testGetAllUsers() throws Exception {
        // Mocking service call
        when(userService.getAllUsers()).thenReturn(Arrays.asList(user1, user2));

        // Performing GET request and asserting the response
        mockMvc.perform(get("/user"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$[0].username").value("user1"))
                .andExpect(jsonPath("$[1].username").value("user2"));

        verify(userService, times(1)).getAllUsers();
    }

    @Test
    void testGetCurrentUser() throws Exception {
        // Mocking the current user from authService
        when(authService.getCurrentUser()).thenReturn(user1);

        // Performing GET request and asserting the response
        mockMvc.perform(get("/user/me"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.username").value("user1"));

        verify(authService, times(1)).getCurrentUser();
    }

    @Test
    void testCreateUser() throws Exception {
        // Mocking service call
        when(userService.createUser(any(User.class))).thenReturn(user1);

        // JSON input for request
        String userJson = "{ \"username\": \"user1\", \"password\": \"password123\" }";

        // Performing POST request and asserting the response
        mockMvc.perform(post("/user/register")
                .contentType(MediaType.APPLICATION_JSON)
                .content(userJson))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.username").value("user1"));

        verify(userService, times(1)).createUser(any(User.class));
    }

    @Test
    void testLogin() throws Exception {
        // Mocking auth service call
        when(authService.verifyUser(any(User.class))).thenReturn("token123");

        // JSON input for request
        String loginJson = "{ \"username\": \"user1\", \"password\": \"password123\" }";

        // Performing POST request and asserting the response
        mockMvc.perform(post("/user/login")
                .contentType(MediaType.APPLICATION_JSON)
                .content(loginJson))
                .andExpect(status().isOk())
                .andExpect(content().string("token123"));

        verify(authService, times(1)).verifyUser(any(User.class));
    }

    @Test
    void testDeleteUser() throws Exception {
        // No mocking needed as delete method has void return type

        // Performing DELETE request and asserting the response
        mockMvc.perform(delete("/user/1"))
                .andExpect(status().isOk());

        verify(userService, times(1)).deleteUser(1L);
    }

    @Test
    void testAddRoleToUser() throws Exception {
        // Mocking service call
        when(userService.addRoleToUser(1L, "ROLE_ADMIN")).thenReturn(user1);

        // Performing PUT request and asserting the response
        mockMvc.perform(put("/user/1/addRole")
                .param("roleToAdd", "ROLE_ADMIN"))
                .andExpect(status().isOk());

        verify(userService, times(1)).addRoleToUser(1L, "ROLE_ADMIN");
    }

    @Test
    void testRemoveRoleFromUser() throws Exception {
        // Mocking service call
        when(userService.removeRoleFromUser(1L, "ROLE_USER")).thenReturn(user1);

        // Performing PUT request and asserting the response
        mockMvc.perform(put("/user/1/removeRole")
                .param("roleToRemove", "ROLE_USER"))
                .andExpect(status().isOk());

        verify(userService, times(1)).removeRoleFromUser(1L, "ROLE_USER");
    }
}






package com.socgen.laxmihealth.meal;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

import com.socgen.laxmihealth.exception.ObjectNotFoundException;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;

import java.util.List;
import java.util.Optional;

class MealServiceTest {

    @Mock
    private MealRepository mealRepository;

    @Mock
    private IngredientRepository ingredientRepository;

    @Mock
    private MealIngredientRepository mealIngredientRepository;

    @InjectMocks
    private MealService mealService;

    private Meal meal1;
    private Meal meal2;
    private Ingredient ingredient;
    private MealIngredient mealIngredient;

    @BeforeEach
    void setUp() {
        meal1 = new Meal();
        meal1.setMealId(1L);
        meal1.setMealName("Meal 1");

        meal2 = new Meal();
        meal2.setMealId(2L);
        meal2.setMealName("Meal 2");

        ingredient = new Ingredient();
        ingredient.setIngredientId(1L);
        ingredient.setIngredientName("Ingredient 1");

        mealIngredient = new MealIngredient();
        mealIngredient.setMeal(meal1);
        mealIngredient.setIngredient(ingredient);
        mealIngredient.setQuantity(2);
    }

    @Test
    void testGetAllMeals() {
        // Mocking repository call
        when(mealRepository.findAll()).thenReturn(List.of(meal1, meal2));

        // Call the service method
        List<Meal> meals = mealService.getAllMeals();

        // Verify the result
        assertEquals(2, meals.size());
        verify(mealRepository, times(1)).findAll();
    }

    @Test
    void testGetMealsByName() {
        // Mocking repository call
        when(mealRepository.findAllByMealName("Meal 1")).thenReturn(List.of(meal1));

        // Call the service method
        List<Meal> meals = mealService.getMealsByName("Meal 1");

        // Verify the result
        assertEquals(1, meals.size());
        assertEquals("Meal 1", meals.get(0).getMealName());
        verify(mealRepository, times(1)).findAllByMealName("Meal 1");
    }

    @Test
    void testCreateMeal() {
        // Mocking repository call
        when(mealRepository.save(meal1)).thenReturn(meal1);

        // Call the service method
        Meal createdMeal = mealService.createMeal(meal1);

        // Verify the result
        assertNotNull(createdMeal);
        assertEquals("Meal 1", createdMeal.getMealName());
        verify(mealRepository, times(1)).save(meal1);
    }

    @Test
    void testAddIngredientToMeal() {
        // Mocking repository calls
        when(mealRepository.findById(1L)).thenReturn(Optional.of(meal1));
        when(ingredientRepository.getIngredientByIngredientId(1L)).thenReturn(ingredient);
        when(mealIngredientRepository.getMealIngredientByIngredientAndMeal(ingredient, meal1))
                .thenReturn(Optional.empty());

        // Call the service method
        Meal updatedMeal = mealService.addIngredientToMeal(1L, 1L, 5);

        // Verify the result
        assertNotNull(updatedMeal);
        assertEquals(1, updatedMeal.getIngredients().size());
        verify(mealRepository, times(1)).findById(1L);
        verify(ingredientRepository, times(1)).getIngredientByIngredientId(1L);
        verify(mealIngredientRepository, times(1))
                .getMealIngredientByIngredientAndMeal(ingredient, meal1);
        verify(mealIngredientRepository, times(1)).save(any(MealIngredient.class));
    }

    @Test
    void testAddIngredientToMeal_ExistingMealIngredient() {
        // Mocking repository calls for an existing meal ingredient
        when(mealRepository.findById(1L)).thenReturn(Optional.of(meal1));
        when(ingredientRepository.getIngredientByIngredientId(1L)).thenReturn(ingredient);
        when(mealIngredientRepository.getMealIngredientByIngredientAndMeal(ingredient, meal1))
                .thenReturn(Optional.of(mealIngredient));

        // Call the service method
        Meal updatedMeal = mealService.addIngredientToMeal(1L, 1L, 10);

        // Verify the result
        assertNotNull(updatedMeal);
        assertEquals(10, mealIngredient.getQuantity());  // Quantity updated
        verify(mealRepository, times(1)).findById(1L);
        verify(ingredientRepository, times(1)).getIngredientByIngredientId(1L);
        verify(mealIngredientRepository, times(1)).getMealIngredientByIngredientAndMeal(ingredient, meal1);
        verify(mealIngredientRepository, times(1)).save(mealIngredient);
    }

    @Test
    void testAddIngredientToMeal_MealNotFound() {
        // Mocking repository call for a missing meal
        when(mealRepository.findById(3L)).thenReturn(Optional.empty());

        // Call the service method and assert exception
        assertThrows(ObjectNotFoundException.class, () -> {
            mealService.addIngredientToMeal(3L, 1L, 5);
        });

        verify(mealRepository, times(1)).findById(3L);
        verify(ingredientRepository, never()).getIngredientByIngredientId(anyLong());
        verify(mealIngredientRepository, never()).getMealIngredientByIngredientAndMeal(any(), any());
    }
}





package com.socgen.laxmihealth.meal;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.socgen.laxmihealth.exception.ObjectNotFoundException;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.ResultActions;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.result.MockMvcResultMatchers;

import java.util.Collections;
import java.util.List;

import static org.mockito.ArgumentMatchers.*;
import static org.mockito.Mockito.*;

@WebMvcTest(controllers = MealController.class)
@AutoConfigureMockMvc
class MealControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private MealService mealService;

    @MockBean
    private IngredientService ingredientService;

    private Meal meal1;

    @BeforeEach
    void setUp() {
        meal1 = new Meal();
        meal1.setMealId(1L);
        meal1.setMealName("Meal 1");
    }

    @Test
    void testGetAllMeals() throws Exception {
        // Mocking service method
        when(mealService.getAllMeals()).thenReturn(Collections.singletonList(meal1));

        // Perform GET request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/meal")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.length()").value(1))
                .andExpect(MockMvcResultMatchers.jsonPath("$[0].mealName").value("Meal 1"));

        // Verify service method invocation
        verify(mealService, times(1)).getAllMeals();
    }

    @Test
    void testGetMealsByName() throws Exception {
        // Mocking service method
        when(mealService.getMealsByName("Meal 1")).thenReturn(Collections.singletonList(meal1));

        // Perform GET request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/meal/name")
                .param("mealName", "Meal 1")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.length()").value(1))
                .andExpect(MockMvcResultMatchers.jsonPath("$[0].mealName").value("Meal 1"));

        // Verify service method invocation
        verify(mealService, times(1)).getMealsByName("Meal 1");
    }

    @Test
    void testCreateMeal() throws Exception {
        // Prepare request body
        ObjectMapper objectMapper = new ObjectMapper();
        String mealJson = objectMapper.writeValueAsString(meal1);

        // Mocking service method
        when(mealService.createMeal(any(Meal.class))).thenReturn(meal1);

        // Perform POST request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.post("/meal")
                .content(mealJson)
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isCreated())
                .andExpect(MockMvcResultMatchers.jsonPath("$.mealName").value("Meal 1"));

        // Verify service method invocation
        verify(mealService, times(1)).createMeal(any(Meal.class));
    }

    @Test
    void testAddIngredientToMeal() throws Exception {
        // Mocking service method
        when(mealService.addIngredientToMeal(eq(1L), eq(2L), eq(5))).thenReturn(meal1);

        // Perform POST request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.post("/meal/1/addIngredient")
                .param("ingredientId", "2")
                .param("quantity", "5")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.mealName").value("Meal 1"));

        // Verify service method invocation
        verify(mealService, times(1)).addIngredientToMeal(eq(1L), eq(2L), eq(5));
    }

    @Test
    void testDeleteIngredient() throws Exception {
        // Mocking service method
        mockMvc.perform(MockMvcRequestBuilders.delete("/meal/ingredient/1")
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(MockMvcResultMatchers.status().isNoContent());

        // Verify service method invocation
        verify(ingredientService, times(1)).deleteIngredientById(eq(1L));
    }

    @Test
    void testDeleteIngredient_NotFound() throws Exception {
        // Mocking service method to throw ObjectNotFoundException
        doThrow(new ObjectNotFoundException("Ingredient", Long.class)).when(ingredientService).deleteIngredientById(eq(1L));

        // Perform DELETE request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.delete("/meal/ingredient/1")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status
        resultActions.andExpect(MockMvcResultMatchers.status().isNotFound());
    }

    @Test
    void testGetIngredientsByName() throws Exception {
        // Mocking service method
        when(ingredientService.getAllIngredientsByName("Ingredient 1")).thenReturn(Collections.singletonList(new Ingredient(1L, "Ingredient 1")));

        // Perform GET request
        ResultActions resultActions = mockMvc.perform(MockMvcRequestBuilders.get("/meal/ingredient/name")
                .param("ingredientName", "Ingredient 1")
                .contentType(MediaType.APPLICATION_JSON));

        // Verify status and content
        resultActions.andExpect(MockMvcResultMatchers.status().isOk())
                .andExpect(MockMvcResultMatchers.jsonPath("$.length()").value(1))
                .andExpect(MockMvcResultMatchers.jsonPath("$[0].ingredientName").value("Ingredient 1"));

        // Verify service method invocation
        verify(ingredientService, times(1)).getAllIngredientsByName("Ingredient 1");
    }
}





# gittest
<div>
  <h2>Add Ingredients to Meal</h2>

  <!-- Search for ingredients -->
  <label for="ingredient-search">Search for an ingredient</label>
  <input type="text" id="ingredient-search" [(ngModel)]="searchTerm" (input)="searchIngredients()">
  
  <!-- Display search results -->
  <ul *ngIf="searchResults.length > 0">
    <li *ngFor="let ingredient of searchResults">
      {{ ingredient.ingredientName }} 
      <button (click)="addIngredient(ingredient)">Add</button>
    </li>
  </ul>

  <!-- List of selected ingredients -->
  <h3>Selected Ingredients</h3>
  <table>
    <thead>
      <tr>
        <th>Ingredient Name</th>
        <th>Quantity</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let ingredient of selectedIngredients">
        <td>{{ ingredient.ingredientName }}</td>
        <td>
          <input type="number" [(ngModel)]="ingredient.quantity">
        </td>
        <td>
          <button (click)="removeIngredient(ingredient)">Remove</button>
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Button to finalize meal -->
  <button (click)="finalizeMeal()">Save Meal</button>
</div>
import { Component, OnInit } from '@angular/core';
import { Ingredient } from './ingredient.model'; // Your ingredient model
import { MealsService } from './meals.service'; // Your service to fetch ingredients

@Component({
  selector: 'app-meal',
  templateUrl: './meal.component.html',
  styleUrls: ['./meal.component.css']
})
export class MealComponent implements OnInit {
  searchTerm: string = '';
  searchResults: Ingredient[] = []; // Search result from the database
  selectedIngredients: { ingredientName: string, ingredientId: number, quantity: number }[] = []; // Ingredients added to the meal

  constructor(private mealsService: MealsService) {}

  ngOnInit(): void {
    // You can load initial data if needed
  }

  // Search for ingredients based on the user's input
  searchIngredients() {
    if (this.searchTerm.trim() === '') {
      this.searchResults = [];
      return;
    }

    this.mealsService.searchIngredients(this.searchTerm).subscribe((results: Ingredient[]) => {
      this.searchResults = results;
    });
  }

  // Add an ingredient to the selected list
  addIngredient(ingredient: Ingredient) {
    this.selectedIngredients.push({
      ingredientId: ingredient.ingredientId,
      ingredientName: ingredient.ingredientName,
      quantity: 1 // Default quantity
    });

    // Clear search
    this.searchResults = [];
    this.searchTerm = '';
  }

  // Remove an ingredient from the list
  removeIngredient(ingredient: any) {
    this.selectedIngredients = this.selectedIngredients.filter(i => i.ingredientId !== ingredient.ingredientId);
  }

  // Finalize the meal and send it to the backend
  finalizeMeal() {
    // Here you can send selectedIngredients to the backend
    console.log('Meal with ingredients', this.selectedIngredients);

    // Save meal using a service or API call
    // mealsService.saveMeal(selectedIngredients).subscribe(...)
  }
}

searchIngredients(term: string): Observable<Ingredient[]> {
  return this.http.get<Ingredient[]>(`${this.baseUrl}/ingredients/search?name=${term}`);
}


@GetMapping("/ingredients/search")
public List<Ingredient> searchIngredients(@RequestParam String name) {
    return ingredientService.searchByName(name); // Implement search logic in service
}


/* Styling for the Add Ingredients section */
.add-ingredients-container {
  margin: 20px 0;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  max-width: 600px;
}

.add-ingredients-container h2 {
  margin-bottom: 20px;
  font-size: 24px;
  color: #333;
}

.add-ingredients-container label {
  font-size: 16px;
  margin-right: 10px;
}

.add-ingredients-container input {
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.add-ingredients-container button {
  padding: 8px 12px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-ingredients-container button:hover {
  background-color: #0056b3;
}

/* Styling for the ingredients list */
.ingredient-list {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

.ingredient-list li {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.ingredient-list li button {
  background-color: #28a745;
  color: white;
  padding: 4px 8px;
  border: none;
  border-radius: 4px;
}

.ingredient-list li button:hover {
  background-color: #218838;
}

/* Styling for the selected ingredients table */
.table-container {
  margin-top: 20px;
}

.table-container table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.table-container th,
.table-container td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.table-container th {
  background-color: #f2f2f2;
  font-size: 18px;
}

.table-container td input {
  width: 60px;
  padding: 5px;
}

.table-container td button {
  padding: 5px 10px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.table-container td button:hover {
  background-color: #c82333;
}

/* Save button styling */
.save-button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.save-button:hover {
  background-color: #0056b3;
}

/* Responsive design */
@media (max-width: 768px) {
  .add-ingredients-container,
  .table-container {
    width: 100%;
  }

  .ingredient-list li {
    flex-direction: column;
    align-items: flex-start;
  }

  .ingredient-list li button {
    margin-top: 5px;
  }
}



<div class="diet-container">
  <!-- Buttons to switch sections -->
  <div>
    <button mat-raised-button color="primary" (click)="showSection('diet')">Diet</button>
    <button mat-raised-button color="accent" (click)="showSection('meal')">Meals</button>
    <button mat-raised-button color="warn" (click)="showSection('ingredient')">Ingredient</button>
  </div>

  <!-- Diet Section -->
  <div *ngIf="selectedSection === 'diet'">
    <mat-form-field appearance="fill">
      <mat-label>Diet Name</mat-label>
      <input matInput id="dietName" formControlName="dietName" />
    </mat-form-field>
  </div>

  <!-- Meal Section -->
  <div *ngIf="selectedSection === 'meal'">
    <mat-tab-group>
      <mat-tab label="Create Meal">
        <div class="meal-container">
          <form (ngSubmit)="addMeal()" #mealForm="ngForm">
            <mat-form-field appearance="fill" class="form-group">
              <mat-label>Meal Name</mat-label>
              <input matInput [(ngModel)]="mealName" name="mealName" required placeholder="Enter the Name of meal">
            </mat-form-field>
            
            <mat-form-field appearance="fill">
              <mat-label>Meal Description</mat-label>
              <input matInput [(ngModel)]="mealDescription" name="mealDescription" required placeholder="Enter the Description">
            </mat-form-field>

            <mat-form-field appearance="fill">
              <mat-label>Calories</mat-label>
              <input matInput type="number" [(ngModel)]="calories" name="calories" required placeholder="Enter Amount of calories">
            </mat-form-field>

            <mat-form-field appearance="fill">
              <mat-label>Protein</mat-label>
              <input matInput type="number" [(ngModel)]="protein" name="protein" required placeholder="Enter Amount of protein">
            </mat-form-field>

            <mat-form-field appearance="fill">
              <mat-label>Fiber</mat-label>
              <input matInput type="number" [(ngModel)]="fibre" name="fibre" required placeholder="Enter Amount of fiber">
            </mat-form-field>

            <mat-form-field appearance="fill">
              <mat-label>Fat</mat-label>
              <input matInput type="number" [(ngModel)]="fat" name="fat" required placeholder="Enter Amount of Fat">
            </mat-form-field>

            <button mat-raised-button color="primary" type="submit" [disabled]="!mealForm.form.valid">Add Meal</button>
          </form>
        </div>
      </mat-tab>

      <!-- Add Ingredients Section -->
      <mat-tab label="Add Ingredients">
        <div *ngIf="isMealAdded" class="add-ingredients-container">
          <mat-form-field appearance="fill">
            <mat-label>Search Ingredient</mat-label>
            <input matInput type="text" [(ngModel)]="searchTerm" (input)="searchIngredients()" placeholder="Search for an Ingredient">
          </mat-form-field>

          <mat-list>
            <mat-list-item *ngFor="let ingredient of searchResults">
              <span matLine>{{ ingredient.ingredientName }}</span>
              <mat-form-field>
                <mat-label>Quantity</mat-label>
                <input matInput type="number" [(ngModel)]="ingredient.quantity" placeholder="Quantity">
              </mat-form-field>
              <button mat-raised-button color="accent" (click)="addIngredient(ingredient)">Add</button>
            </mat-list-item>
          </mat-list>
        </div>
      </mat-tab>

      <!-- Selected Ingredients Table -->
      <mat-tab label="Selected Ingredients">
        <div *ngIf="selectedIngredients.length > 0" class="table-container">
          <h3>Selected Ingredients</h3>
          <table mat-table [dataSource]="selectedIngredients" class="mat-elevation-z8">
            <ng-container matColumnDef="ingredientName">
              <th mat-header-cell *matHeaderCellDef> Ingredient Name </th>
              <td mat-cell *matCellDef="let element"> {{element.ingredientName}} </td>
            </ng-container>

            <ng-container matColumnDef="quantity">
              <th mat-header-cell *matHeaderCellDef> Quantity </th>
              <td mat-cell *matCellDef="let element">
                <input matInput type="number" [(ngModel)]="element.quantity">
              </td>
            </ng-container>

            <ng-container matColumnDef="actions">
              <th mat-header-cell *matHeaderCellDef> Actions </th>
              <td mat-cell *matCellDef="let element">
                <button mat-raised-button color="warn" (click)="removeIngredient(element)">Remove</button>
                <button mat-raised-button color="primary">Add to Meal</button>
              </td>
            </ng-container>

            <tr mat-header-row *matHeaderRowDef="['ingredientName', 'quantity', 'actions']"></tr>
            <tr mat-row *matRowDef="let row; columns: ['ingredientName', 'quantity', 'actions']"></tr>
          </table>
        </div>
      </mat-tab>
    </mat-tab-group>
  </div>
</div>
<div class="diet-container">

  <div>
    <button type="button" (click)="showSection(section: 'diet')">Diet</button>
    <button type="button" class="btn btn-secondary" (click)="showSection(section: 'meal')">Meals</button>
    <button type="button" class="btn btn-secondary" (click)="showSection(section: 'ingredient')">Ingredient</button>
  </div>

  <div *ngIf="selectedSection==='diet'">
    <label for="dietName">Diet Name</label>
    <input id="dietName" formControlName="dietName" />
  </div>

  <div *ngIf="selectedSection==='meal'">
    <mat-tab-group>
      <mat-tab label="Create Meal">
        <div class="meal-container" style="margin-left: 428px;">
          <form (ngSubmit)="addMeal()" #mealForm="ngForm">
            <div class="form-group col-lg-12">
              <input [(ngModel)]="mealName" name="mealName" class="form-control" placeholder="Enter the Name of meal" required>
            </div>
            <div class="form-group">
              <input [(ngModel)]="mealDescription" name="mealDescription" class="form-controli" placeholder="Enter the Description" required>
            </div>
            <div class="form-group">
              <input [(ngModel)]="calories" name="calories" class="form-control1" placeholder="Enter Amount of calories" required>
            </div>
            <div class="form-group">
              <input [(ngModel)]="protein" name="protein" class="form-control" placeholder="Enter Amount of protein" required>
            </div>
            <div class="form-group">
              <input [(ngModel)]="fibre" name="fibre" class="form-control1" placeholder="Enter Amount of fiber" required>
            </div>
            <div class="form-group">
              <input [(ngModel)]="fat" name="fat" placeholder="Enter Amount of Fat" required>
            </div>
            <div>
              <button class="btn btn-outline-primary" type="submit" [disabled]="!mealForm.form.valid">Add meal</button>
            </div>
          </form>
        </div>
      </mat-tab>

      <mat-tab label="Add Ingredients">
        <div *ngIf="isMealAdded" class="add-ingredients-container-search">
          <ul class="ingredient-list">
            {{ingredient.ingredientName}}
            <label for="ingredient-search" class="add-ingredients-container-label">Search for an Ingredient</label>
            <input type="text" id="ingredient-search" [(ngModel)]="searchTerm" name="searchTerm" (input)="searchIngredients()" placeholder="Search" class="add-ingredients-container-input">
            <li *ngFor="let ingredient of searchResults">
              {{ingredient.ingredientId}}
              <input type="number" placeholder="Quantity" [ngModel]="quantity"/>
              <button (click)="addIngredient(ingredient)" class="add-ingredients-container-button">Add</button>
            </li>
          </ul>
        </div>
      </mat-tab>

      <mat-tab label="Selected Ingredients">
        <div class="table-container" *ngIf="selectedIngredients.length>0">
          <h3 class="SelectedIn">Selected Ingredient</h3>
          <table>
            <thead>
              <tr>
                <th>Ingredient Name</th>
                <th>Quantity</th>
                <th>Action</th>
                <th>Add to Meal</th>
              </tr>
            </thead>
            <tbody>
              <tr *ngFor="let ingredient of selectedIngredients">
                <td style="color: white">{{ ingredient.ingredientName }}</td>
                <td>
                  <input type="number" [(ngModel)]="ingredient.quantity" name="quantity_{{ingredient.ingredientId}}" placeholder="Quantity">
                </td>
                <td>
                  <button (click)="removeIngredient(ingredient)">Remove</button>
                </td>
                <td>
                  <button class="add-ingredients-container-button" style="background-color:lawngreen">Add</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </mat-tab>
    </mat-tab-group>
  </div>
</div>



<mat-tab-group (selectedTabChange)="onTabChange($event)">
  <mat-tab label="Create Meal">
    <!-- Create Meal Content Here -->
  </mat-tab>

  <mat-tab label="Display Meal">
    <!-- Display Meal Table -->
    <div *ngIf="meals.length > 0" class="table-container">
      <h3>Available Meals</h3>
      <table class="table table-striped">
        <thead>
          <tr>
            <th>Meal Name</th>
            <th>Calories</th>
            <th>Protein</th>
            <th>Fibre</th>
            <th>Fat</th>
            <th>Ingredients</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let meal of meals">
            <td>{{ meal.mealName }}</td>
            <td>{{ meal.calories }}</td>
            <td>{{ meal.protein }}</td>
            <td>{{ meal.fibre }}</td>
            <td>{{ meal.fat }}</td>
            <td>
              <ul>
                <li *ngFor="let ingredient of meal.ingredients">{{ ingredient.ingredientName }} - {{ ingredient.quantity }}</li>
              </ul>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </mat-tab>
</mat-tab-group>



  getAllMeals(): Observable<any> {
    return this.http.get(`${this.baseUrl}/meals`);  // Adjust URL according to your backend API
  }

  // Method to load meals when the tab is selected
  loadMeals() {
    this.getAllMeals().subscribe(
      (data: any[]) => {
        this.meals = data;
        console.log('Meals fetched:', this.meals);
      },
      (error) => {
        console.error('Error fetching meals:', error);
      }
    );
  }


  onTabChange(event: any): void {
  // Check if the Display Meal tab is selected
  if (event.index === 1) {
    this.loadMeals();
  }
}


<div>
  <form [formGroup]="dietForm" (ngSubmit)="onSubmit()">
    <label for="dietName">Diet Name</label>
    <input id="dietName" formControlName="dietName" />

    <label for="dietType">Diet Type</label>
    <input id="dietType" formControlName="dietType" />

    <label for="dietDescription">Diet Description</label>
    <textarea id="dietDescription" formControlName="dietDescription"></textarea>

    <label for="dietMeal">Search Meals</label>
    <input type="text" (input)="onMealSearch($event.target.value)" placeholder="Search meals by name" />
    <div *ngIf="filteredMeals.length > 0">
      <ul>
        <li *ngFor="let meal of filteredMeals" (click)="addMealToDiet(meal)">
          {{ meal.mealName }}
        </li>
      </ul>
    </div>

    <button type="submit">Create Diet</button>
  </form>

  <!-- Table to display diets -->
  <div>
    <table>
      <thead>
        <tr>
          <th>Diet Name</th>
          <th>Meal Name</th>
          <th>Ingredient Name</th>
        </tr>
      </thead>
      <tbody>
        <tr *ngFor="let diet of diets">
          <td>{{ diet.dietName }}</td>
          <td>{{ diet.meals.map(m => m.mealName).join(', ') }}</td>
          <td>{{ diet.meals.map(m => m.ingredients.map(i => i.name).join(', ')).join(', ') }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>


<div *ngIf="selectedSection==='diet'">
  <div class="row" style="margin-top: 6vh">
    
    <!-- Display meals -->
    <div class="col-sm-6">
      <ul class="Meal-list">
        <li class="row" *ngFor="let meal of searchMealResult">
          <div class="col-md-4">{{ meal.mealName }}</div>
          <div class="col-md-4">{{ meal.ingredients }}</div>
          <div>
            <button (click)="selectMeal(meal)"> ADD Meal</button>
          </div>
        </li>
      </ul>
    </div>

    <!-- Display diets in a table -->
    <div class="col-sm-6">
      <table class="table">
        <thead>
          <tr>
            <th>Diet Name</th>
            <th>Diet Type</th>
            <th>Diet Description</th>
            <th>Meals</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let diet of diets">
            <td>{{ diet.dietName }}</td>
            <td>{{ diet.dietType }}</td>
            <td>{{ diet.dietDescription }}</td>
            <td>
              <ul>
                <li *ngFor="let meal of diet.dietMeals">
                  {{ meal.mealName }}
                </li>
              </ul>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    
  </div>
</div>



package com.socgen.laxmihealth.diet;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;
import org.springframework.boot.test.context.SpringBootTest;
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

@SpringBootTest
class DietServiceTest {

    @Mock
    private DietRepository dietRepository;

    @InjectMocks
    private DietService dietService;

    private Diet diet1;
    private Diet diet2;

    @BeforeEach
    void setUp() {
        MockitoAnnotations.openMocks(this);
        
        diet1 = new Diet();
        diet1.setDietId(1L);
        diet1.setDietName("Keto");

        diet2 = new Diet();
        diet2.setDietId(2L);
        diet2.setDietName("Vegan");
    }

    @Test
    void testGetAllDiets() {
        // Mocking repository to return a list of diets
        when(dietRepository.findAll()).thenReturn(Arrays.asList(diet1, diet2));

        // Call the service method
        List<Diet> dietList = dietService.getAllDiets();

        // Asserts
        assertEquals(2, dietList.size());
        verify(dietRepository, times(1)).findAll();
    }

    @Test
    void testGetDietById() {
        // Mocking repository to return a diet by its ID
        when(dietRepository.findById(1L)).thenReturn(Optional.of(diet1));

        // Call the service method
        Diet foundDiet = dietService.getDietById(1L);

        // Asserts
        assertNotNull(foundDiet);
        assertEquals("Keto", foundDiet.getDietName());
        verify(dietRepository, times(1)).findById(1L);
    }

    @Test
    void testCreateOrUpdateDiet() {
        // Mocking repository to save a diet
        when(dietRepository.save(diet1)).thenReturn(diet1);

        // Call the service method
        Diet savedDiet = dietService.createOrUpdateDiet(diet1);

        // Asserts
        assertNotNull(savedDiet);
        assertEquals("Keto", savedDiet.getDietName());
        verify(dietRepository, times(1)).save(diet1);
    }

    @Test
    void testDeleteDietById() {
        // Call the service method
        dietService.deleteDietById(1L);

        // Verifies the delete method is called once
        verify(dietRepository, times(1)).deleteById(1L);
    }

    @Test
    void testDietNotFound() {
        // Mocking repository to return an empty Optional when diet is not found
        when(dietRepository.findById(3L)).thenReturn(Optional.empty());

        // Call the service method and expect an exception
        assertThrows(ObjectNotFoundException.class, () -> dietService.getDietById(3L));
    }
}
