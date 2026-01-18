import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class EditableProfileUI extends JFrame {

    // Labels
    private JLabel nameLabel, usernameLabel, bioLabel, followersLabel, followingLabel;

    // Text fields
    private JTextField nameField, usernameField, followersField, followingField;
    private JTextArea bioArea;

    // Buttons
    private JButton editButton, saveButton;

    public EditableProfileUI() {
        setTitle("Editable Profile");
        setSize(420, 650);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // ===== HEADER =====
        JPanel header = new JPanel();
        header.setBackground(new Color(255, 165, 90));
        header.setPreferredSize(new Dimension(420, 120));
        header.add(new JLabel("PROFILE"));
        add(header, BorderLayout.NORTH);

        // ===== MAIN PANEL =====
        JPanel mainPanel = new JPanel();
        mainPanel.setLayout(new BoxLayout(mainPanel, BoxLayout.Y_AXIS));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(15, 15, 15, 15));

        // Name
        nameLabel = new JLabel("Marl Vyreigh");
        nameField = new JTextField("Marl Vyreigh");
        toggleField(nameField, false);

        // Username
        usernameLabel = new JLabel("@crzyreiighhh");
        usernameField = new JTextField("@crzyreiighhh");
        toggleField(usernameField, false);

        // Bio
        bioLabel = new JLabel("Life’s a bore if you don’t challenge yourself");
        bioArea = new JTextArea("Life’s a bore if you don’t challenge yourself");
        bioArea.setLineWrap(true);
        bioArea.setWrapStyleWord(true);
        bioArea.setEnabled(false);

        // Followers
        followersLabel = new JLabel("Followers: 167");
        followersField = new JTextField("167");
        toggleField(followersField, false);

        // Following
        followingLabel = new JLabel("Following: 328");
        followingField = new JTextField("328");
        toggleField(followingField, false);

        // Buttons
        editButton = new JButton("Edit Profile");
        saveButton = new JButton("Save");
        saveButton.setEnabled(false);

        // ===== ADD COMPONENTS =====
        mainPanel.add(nameLabel);
        mainPanel.add(nameField);
        mainPanel.add(Box.createVerticalStrut(8));

        mainPanel.add(usernameLabel);
        mainPanel.add(usernameField);
        mainPanel.add(Box.createVerticalStrut(8));

        mainPanel.add(new JLabel("Bio:"));
        mainPanel.add(new JScrollPane(bioArea));
        mainPanel.add(Box.createVerticalStrut(8));

        mainPanel.add(followersLabel);
        mainPanel.add(followersField);
        mainPanel.add(Box.createVerticalStrut(8));

        mainPanel.add(followingLabel);
        mainPanel.add(followingField);
        mainPanel.add(Box.createVerticalStrut(15));

        mainPanel.add(editButton);
        mainPanel.add(saveButton);

        add(mainPanel, BorderLayout.CENTER);

        // ===== BUTTON LOGIC =====
        editButton.addActionListener(e -> enableEditing(true));

        saveButton.addActionListener(e -> {
            nameLabel.setText(nameField.getText());
            usernameLabel.setText(usernameField.getText());
            bioLabel.setText(bioArea.getText());
            followersLabel.setText("Followers: " + followersField.getText());
            followingLabel.setText("Following: " + followingField.getText());

            enableEditing(false);
        });

        setVisible(true);
    }

    // Enable / Disable fields
    private void enableEditing(boolean enable) {
        nameField.setEnabled(enable);
        usernameField.setEnabled(enable);
        bioArea.setEnabled(enable);
        followersField.setEnabled(enable);
        followingField.setEnabled(enable);

        saveButton.setEnabled(enable);
        editButton.setEnabled(!enable);
    }

    private void toggleField(JTextField field, boolean enabled) {
        field.setMaximumSize(new Dimension(Integer.MAX_VALUE, 28));
        field.setEnabled(enabled);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(EditableProfileUI::new);
    }
}
