import org.springframework.jdbc.core.JdbcTemplate;

public class EmployeeDao {
    private JdbcTemplate jdbcTemplate;

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    // Create (Insert)
    public void save(Employee employee) {
        String sql = "INSERT INTO employee (id, name, age) VALUES (?, ?, ?)";
        jdbcTemplate.update(sql, employee.getId(), employee.getName(), employee.getAge());
    }

    // Read (Select)
    public Employee getById(int id) {
        String sql = "SELECT * FROM employee WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, new EmployeeRowMapper());
    }

    // Update
    public void update(Employee employee) {
        String sql = "UPDATE employee SET name = ?, age = ? WHERE id = ?";
        jdbcTemplate.update(sql, employee.getName(), employee.getAge(), employee.getId());
    }

    // Delete
    public void delete(int id) {
        String sql = "DELETE FROM employee WHERE id = ?";
        jdbcTemplate.update(sql, id);
    }
}
